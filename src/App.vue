<template>
  <div id="app">
    <transition name="fade">
      <preloader 
        v-show="activePage == pages.preloader"></preloader>
    </transition>

    <div class="pages">
      <transition name="fade">
        <page-title
          v-show="activePage == pages.title" 

          @click="activePage = pages.login">
        </page-title>
      </transition>

      <transition name="fade">
        <page-login
          v-show="activePage == pages.login"

          @login="activePage=pages.photo"
          >
        </page-login>
      </transition>

      <transition name="fade">
        <page-photo
          v-show="activePage == pages.photo"
 
          @rated="activePage=pages.main"
          >
        </page-photo>
      </transition>

      <transition name="fade">
        <page-main
          v-show="activePage == pages.main"
 
          @publish="activePage=pages.result"
          >
        </page-main>
      </transition>

      <transition name="fade">
        <page-result
          v-show="activePage == pages.result"
 
          @send="activePage=pages.list"
          @cancel="activePage=pages.main"
          >
        </page-result>
      </transition>

      <transition name="fade">
        <page-list
          v-show="activePage == pages.list"
 
          @click="activePage=pages.listView"
          @back="activePage=pages.result"
          >
        </page-list>
      </transition>

      <transition name="fade">
        <page-list-view
          v-show="activePage == pages.listView"

          @back="activePage=pages.list"
          >
        </page-list-view>
      </transition>

      <transition name="fade">
        <page-visionhub-test
          v-show="activePage == pages.visionhubTest"

          @start="activePage=pages.title"
          >
        </page-visionhub-test>
      </transition>
    </div>

  </div>
</template>

<script>
import Preloader from './components/Preloader'
import PageTitle from './components/PageTitle'
import PageLogin from './components/PageLogin'
import PagePhoto from './components/PagePhoto'
import PageMain from './components/PageMain'
import PageResult from './components/PageResult'
import PageList from './components/PageList'
import PageListView from './components/PageListView'
import PageVisionhubTest from './components/PageVisionhubTest';

export default {
  name: 'app',
  components: {
    'preloader': Preloader,
    'page-title': PageTitle,
    'page-login': PageLogin,
    'page-photo': PagePhoto,
    'page-main': PageMain,
    'page-result': PageResult,
    'page-list': PageList,
    'page-list-view': PageListView,
    'page-visionhub-test': PageVisionhubTest,
  },
  created() {
    setTimeout( () => {
      // this.activePage = this.pages.title;
      this.activePage = this.pages.visionhubTest;
    }, 700 );
  },
  watch: {
    activePage(val) {
      var  intrvl1, intrvl2;
      if ( val == this.pages.photo ) {
        intrvl1 = setInterval(() => {
          this.$root.$data.raiting = this.$root.$data.raiting - Math.floor(Math.random()*3);
          if (this.$root.$data.raiting <= 1) {
            this.$root.$data.raiting = 1;
            clearInterval(intrvl1);
          }
        }, 3000);

        intrvl2 = setInterval(() => {
          this.$root.$data.raiting = this.$root.$data.raiting - Math.ceil(Math.random()*5);
          if (this.$root.$data.raiting <= 1) {
            this.$root.$data.raiting = 1;
            clearInterval(intrvl1);
            clearInterval(intrvl2);
          }
        }, 10000);
      }
    }
  },
  data () {
    return {
      activePage: -1,

      pages: {
        preloader: -1,
        title: 0,
        login: 1,
        photo: 2,
        main: 3,
        result: 4,
        list: 5,
        listView: 6,
        
        visionhubTest: 7,
      }
    }
  },
  methods: {
  }
}
</script>

<style scoped>
  #app {
    height: 100%;
  }

.fade-enter-active, .fade-leave-active {
    transition: opacity .5s ease;
}
.fade-enter, .fade-leave-to {
    opacity: 0;
    position: absolute;

}

.fade-enter-to, .fade-leave {
    opacity: 1;
    position: relative;
}
</style>

