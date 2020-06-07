<template>
    <div class="list_page_add main_container">
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
                </div>
            </div>
        </header>
        <div class="main_content">
            <div class="main_content_wrap">
                <div class="row">
                    <div class="col-sm-12">
                        <div class="add_title_wrap">
                            <h3 class="add_title">Хакатон 2020</h3>
                        </div>
                        <div class="list_game_add">
                            <div class="list_game_add_itm"><img src="../img/personal.jpg" alt="" class="list_game_image">

                            </div>
                            <div class="list_game_add_itm"><img src="../img/personal.jpg" alt="" class="list_game_image">

                            </div>
                            <div class="list_game_add_itm"><img src="../img/personal.jpg" alt="" class="list_game_image">

                            </div>
                            <div class="list_game_add_itm"><img src="../img/personal.jpg" alt="" class="list_game_image">

                            </div>
                            <div class="list_game_add_itm"><img src="../img/personal.jpg" alt="" class="list_game_image">

                            </div>
                            <div class="list_game_add_itm"><img src="../img/personal.jpg" alt="" class="list_game_image">

                            </div>
                            <div class="list_game_add_itm"><img src="../img/personal.jpg" alt="" class="list_game_image">

                            </div>
                            <div class="list_game_add_itm"><img src="../img/personal.jpg" alt="" class="list_game_image">

                            </div>
                            <div class="list_game_add_itm"><img src="../img/personal.jpg" alt="" class="list_game_image">

                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="main_content_wrap"><div class="row">
                <div class="col-sm-12">
                    <div class="main_btn_wrap">
                        <button 
                            @click="$emit('back')"
                            class="main_btn"
                            >
                                Вернуться
                        </button>
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
        }
    }
}
</script>