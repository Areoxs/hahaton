<template>
    <div class="main_page main_container">
        <header class="main_header main_header-circle">
            <div class="container-fluid">
                <div class="row">
                    <div class="col-sm-12">
                        <div class="top_line">
                            <div class="top_line_itm"><div class="user_text_wrap">
                                <span class="user_text">{{ name }}</span>
                            </div></div>
                            <div class="top_line_itm">
                                <div class="personal_icon_wrap">
                                    <img src="../img/icon_pecs.png" alt="" class="personal_icon">
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-sm-12">
                        <div class="static_cont">
                            <div class="static_wrap">
                                <div class="static_itm static_itm_green">
                                    <h2 class="static_title"><img src="../img/statistic.svg" alt=""><span>Статистика</span></h2>
                                    <div class="static_info">
                                        <p class="static_figure">111</p>
                                        <p class="static_text">фото</p>
                                    </div>
                                </div>
                                <div class="static_itm static_itm_blue">
                                    <h2 class="static_title"><img src="../img/happy.svg" alt=""><span>Популярность</span></h2>
                                    <div class="static_info">
                                        <p class="static_figure">{{ raiting }}</p>
                                        <p class="static_text">Место в рейтинге</p>
                                    </div>
                                </div>
                            </div>


                        </div>
                    </div>
                </div>
            </div>
        </header>
        <div class="main_content">
            <div class="main_content_wrap">
                <div class="row">
                    <div class="col-sm-12">
                        <div class="main_action_wrap">
                            <div class="main_action_itm">
                                <label for="camera_hold" class="main_action_btn">
                                    <span class="main_action_icon"><i class="fa fa-camera-retro" aria-hidden="true"></i></span>
                                    <input 
                                        ref="camera"
                                        @change="setCameraImage" 
                                        type="file" 
                                        id="camera_hold" 
                                        accept="image/*;capture=camera" 
                                        class="hidden_file">
                                    <span>Сделать фото</span>
                                </label>
                            </div>
                            <div class="main_action_itm">
                                <label for="gallery_hold" class="main_action_btn">
                                    <span class="main_action_icon"><i class="fa fa-picture-o" aria-hidden="true"></i></span>
                                    <input 
                                        ref="gallery"
                                        @change="serGalleryImage"
                                        type="file" 
                                        id="gallery_hold" 
                                        class="hidden_file">
                                    <span>Галерея</span>
                                </label>

                            </div>
                        </div>
                    </div>


                </div>
            </div>
            <div class="main_content_wrap">
                <div class="row"><div class="col-sm-12">
                    <div class="prepare_img_wrap">
                        <img v-if="!image" src="../img/place_photo.png" alt="" class="prepare_img">
                        <img v-else
                            :src="image" 
                            alt="" class="prepare_img">
                    </div>
                </div></div>

            </div>
            <div class="main_content_wrap"><div class="row">
                <div class="col-sm-12">
                    <div class="main_btn_wrap">
                        <button 
                            @click="$emit('publish')"
                            class="main_btn">опубликовать</button>
                    </div>
                </div>
            </div></div>

        </div>

    </div>
</template>

<script>
export default {
    computed: {
        name() {
            return !!this.$root.$data.name
                ? this.$root.$data.name
                : "Иванов Иван Иваныч";
        },
        raiting() {
            return  this.$root.$data.raiting;
        },
        image: {
            get() {
                return this.$root.$data.image;
            },
            set(val) {
                this.$root.$data.image= val;
            }
        },

    },
    methods: {
        setCameraImage() {
            var file = this.$refs.camera.files[0];
            this.image = URL.createObjectURL(file);
        },
        serGalleryImage() {
            var file = this.$refs.gallery.files[0];
            this.image = URL.createObjectURL(file);
        }
    }
}
</script>