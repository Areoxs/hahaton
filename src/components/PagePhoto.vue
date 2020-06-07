<template>
    <div class="photo_page main_container">
        <header class="main_header main_header-static main_header-circle">
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
                        <div class="hint_wrap">
                            <p class="hint_text">Если нравится фото, смахните вправо или нажмите “нравится</p>
                        </div>
                    </div>
                </div>
            </div>
        </header>
        <div class="main_content">
            <div class="huge_photo">
                <div class="huge_photo_itm">

                </div>
                <div class="main_btn_wrap">
                    <button class="main_btn main_btn_red">Убрать</button>
                    <button 
                        @click="$emit('rated')"
                        class="main_btn"
                        >
                            Нравится
                    </button>
                </div>
            </div>
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
        }
    }
    
}
</script>