<template>
    <div class="second_page main_container large_bg">
        <header class="main_header">
            <div class="container-fluid">
                <div class="row">
                    <div class="col-sm-12">
                        <div class="logo_wrap">
                            <a href="#" class="logo">
                                <img src="../img/logo_text_new.svg" alt="">
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </header>
        <div class="main_content">
            <div class="container-fluid">
                <div class="row">
                    <div class="col-sm-12">
                        <div class="login_cont">
                            <form 
                                @submit.prevent 
                                class="login_form"
                                >
                                    <div class="login_title">
                                        Авторизуйтесь
                                    </div>
                                    <div class="input-field">
                                        <label for="login">
                                            <input 
                                                v-model="$root.$data.name"
                                                type="text" 
                                                id="login" 
                                                class="main_input" 
                                                placeholder="Введите ваше ФИО"
                                                >
                                        </label>
                                    </div>
                                    <div class="login_text">
                                        <span>или</span>
                                    </div>
                                    <div class="login_icon_wrap">
                                        <a href="#" class="login_icon">
                                            <i class="fa  fa-vk "></i>
                                        </a><a href="#" class="login_icon">

                                        <i class="fa  fa-instagram "></i>
                                    </a><a href="#" class="login_icon">
                                        <i class="fa fa-twitter"></i>
                                    </a>
                                    </div>
                                    <div class="login_btn_wrap">
                                        <button 
                                            @click="$emit('login')"
                                            class="main_btn main_btn_red"
                                            >
                                                Войти
                                        </button>
                                    </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    
}
</script>