<template>
    <div
        @click="$emit('click')" 
        class="first_page main_container large_bg"
        >
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
                        <div class="welcome_cont">
                            <h3 class="main_title">Ха-ха-тон<br> 2020
                            </h3>
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