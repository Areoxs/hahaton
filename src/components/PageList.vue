<template>
    <div class="list_page main_container">
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
                            <h3 class="add_title">Участник публикаций</h3>
                        </div>
                        <div class="list_game">
                            <div
                                @click="$emit('click')" 
                                class="list_game_itm"
                                >
                                    <img src="../img/personal.jpg" alt="" class="list_game_image">
                                    <div class="list_game_info">
                                        <div class="list_game_info_title">хакатон 2020</div>
                                        <div class="list_game_info_hash">#hahaton2020</div>
                                    </div>
                            </div>
                            <!--div class="list_game_itm"><img src="../img/personal.jpg" alt="" class="list_game_image">
                                <div class="list_game_info">
                                    <div class="list_game_info_title">хакатон 2020</div>
                                    <div class="list_game_info_hash">#hahaton2020</div>
                                </div>
                            </div-->
                        </div>
                    </div>
                </div>
            </div>
            <div class="main_content_wrap">
                <div class="row">
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