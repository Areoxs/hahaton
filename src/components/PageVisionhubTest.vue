<template>
  <div id="vh-test">
    <img src="../assets/logo.png">
    <h1>{{ msg }}</h1>
    <button 
      @click="$emit('start')"
      class="main_btn main_btn_red"
      >
        Макет
    </button>
    <form @submit.prevent>
      <p><b>Выбор модели</b></p>
      <ul>
        <li>
          <label>
              <input v-model="visionhub.model" name="model" type="radio" value="pixel-art"> 
              Пиксель арт
          </label>
        </li>
        <li>
          <label>
            <input v-model="visionhub.model" name="model" type="radio" value="anime-selfie">
            Аниме
          </label>
        </li>
        <li>
          <label>
            <input v-model="visionhub.model" name="model" type="radio" value="animal-gan" checked> 
            Животное
          </label>
        </li>
      </ul>
      <p><b>Фото</b></p>
      <p>
        <input
          ref="file" 
          @change="handleFileUpload()"

          name="image" 
          type="file"> 
      </p>

      <p>
        <input 
          @click="sendForm()" 
          
          type="submit" 
          value="Обработать"
          class="main_btn">
      </p>
      <p style="color: red">{{errorMsg}}</p>
      <canvas ref=canvas></canvas>
      <img 
        v-show="showPreview"
        :src="imagePreview" 
        />

    </form>
  </div>
</template>

<script>
var debug = true;

import axios from 'axios';

export default {
  created() {
    this.getVisionhubToken();   
  },
  data () {
    return {
      msg: 'Хахатон',
      errorMsg: "",

      showPreview: false,
      imagePreview: null,

      visionhub: {
        token: null,
        model: null,
        image: null,
        task: null,
        resultUrl: null,
      }
    }
  },
  methods: {
    getVisionhubToken() {
      if (debug) console.log('getToken', !localStorage.token , localStorage.tokenExpiresTime < Date.now())
      // Если уже генерили токен, берем из localStorage
      if (!localStorage.token || localStorage.tokenExpiresTime < Date.now()) {
        axios.get('https://www.visionhub.ru/api/v2/auth/generate_token/')
          .then( response => {
            if (debug) console.log(response);
            var token = response.data.token;
            var oneHour = 1000 * 60 * 60;

            this.visionhub.token = token;
            localStorage.token = token;
            localStorage.tokenExpiresTime = Date.now() + oneHour;
          });
      } else {
        this.visionhub.token = localStorage.token;
      }
    },
    handleFileUpload() {
      if (debug) console.log('upload', this.$refs.file.files[0]);
      var file = this.$refs.file.files[0];

      this.scaleImage( file, 480);
    },
    scaleImage( file, size ) {
      var imgSrc = URL.createObjectURL(file);
      const img = new Image();

      var canvas = this.$refs.canvas;
      var context = canvas.getContext('2d');

      img.onload = () => {
        var scale = size / img.naturalWidth;

        var scaledWidth = img.naturalWidth * scale;
        var scaledHeight = img.naturalHeight * scale;

        canvas.width=scaledWidth;
        canvas.height=scaledHeight;

        context.drawImage(img, 0, 0, scaledWidth, scaledHeight);
        
        this.visionhub.image = this.dataURLtoBlob(canvas.toDataURL("image/jpeg", 1));

      }
      img.src = imgSrc;
    },
    dataURLtoBlob(dataURI) {
      var binary = atob(dataURI.split(',')[1]);
      var array = [];
      for(var i = 0; i < binary.length; i++) {
          array.push(binary.charCodeAt(i));
      }
      return new Blob([new Uint8Array(array)], {type: 'image/jpeg'});
    },
    sendForm(){
      let formData = new FormData();
      this.errorMsg = "";

      formData.append('model', this.visionhub.model);
      formData.append('image', this.visionhub.image, "1.jpg");

      axios.post( 'https://www.visionhub.ru/api/v2/process/img2img/',
        formData,
        {
          headers: {
              'Authorization': 'Bearer ' + this.visionhub.token,
              'Content-Type': 'multipart/form-data'
          }
        })
        .then( response => {
          console.log('SUCCESS!!', response);
          this.visionhub.task = response.data.task_id;

          this.getTaskResult( this.visionhub.task );
        })
        .catch( response => {
          console.log('FAILURE!!', response);
          this.errorMsg = response;
        });
    },
    getTaskResult( id ) {
      if (debug) console.log('getTaskResult');
      var checkTaskInterval;

      checkTaskInterval = setInterval( () => {
        this.checkTask(id)
          .then( success => {
            clearInterval(checkTaskInterval);

            this.visionhub.resultUrl = success.url;
            this.getProcessedImage(this.visionhub.resultUrl);           
          });
      }, 3000 );
    },
    checkTask(id) {
      return new Promise( (resolve,reject) => {
        if (debug) console.log('checkTask', this.visionhub.task);

        axios.get('https://www.visionhub.ru/api/v2/task_result/' + this.visionhub.task,
          {
            headers: {
              'Authorization': 'Bearer ' + this.visionhub.token,
            }
          })
          .then( response => {
            if (response.data.status == "DONE") {
              if (debug) console.log('checkTask > DONE', response.data.url);

              resolve(response.data);
            } else {
              if (debug) console.log('checkTask > waiting', response.data);

              // reject();
            }
          })
      }); 
    },
    getProcessedImage( resultUrl ) {
      if (debug) console.log('getProcessedImage', 'https://www.visionhub.ru' + resultUrl);

        axios.request({
          method: 'GET',
          url: 'https://www.visionhub.ru' + resultUrl,
          responseType: 'arraybuffer',
          responseEncoding: 'binary',
          headers:{
            'Authorization': 'Bearer ' + this.visionhub.token,
            'Content-type': 'image/jpg',
          }
        })
        .then( response => {
          let blob = new Blob([response.data]);
          let reader = new FileReader();
          
          reader.readAsArrayBuffer(blob);

          reader.addEventListener("load", () => {
            this.showPreview = true;
            this.imagePreview = "data:image/jpeg;base64," + btoa(String.fromCharCode.apply(null, new Uint8Array(reader.result))); // to base64 
          }, false);

        });
    },
  }
}
</script>

<style lang="scss">
#vh-test {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
