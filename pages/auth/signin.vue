<template>
    <div id="signInContent"
        class="h-[100dvh] w-full grid grid-cols-1 md:grid-cols-2 justify-items-center place-items-center md:p-0 p-8">
        <div v-if="loadImg" :data-aos="fadeAnimate" class="w-full hidden md:grid justify-items-center md:justify-items-start md:place-items-center">
            <div :class="imgBgClass">
                <div id="loginLayoutBlurWrapper" class="min-h-[100dvh] w-full duration-[600ms] ease-in-out" :class="blurWrapperClass"/>
            </div>
        </div>
        <div class="invisible" v-else />
        <div class="w-full grid justify-items-center space-y-8 md:px-8">
            <img src="/logo/foonyew.png" class="w-40">
            <h1 v-if="embedLogin" class="mt-3 text-3xl zhHans-bold">登入</h1>
            <div v-else class="mt-3 w-full grid grid-cols-2">
                <div class="w-full grid justify-items-start place-items-center">
                    <button @click="$router.go('/passport')" class="flex px-4 py-2 rounded-2xl bg-white hover:brightness-95 active:brightness-75 active:scale-95 duration-200 ease-in-out">
                        <i class="fas fa-chevron-left my-auto mr-2" />
                        返回
                    </button>
                </div>
                <div class="w-full grid justify-items-end place-items-center">
                    <button class="flex px-4 py-2 rounded-2xl bg-white hover:brightness-95 active:brightness-75 active:scale-95 duration-200 ease-in-out">
                        <i class="fas fa-ellipsis-vertical my-auto" />
                    </button>
                </div>
            </div>
            <input v-model="inputValue.username" placeholder="用户名/电子邮件"
            v-if="!showPasswordInputs"
                class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
            <div v-if="embedLogin" class="w-full grid justify-items-center place-items-center">
            <input v-if="inputState.password" v-model="inputValue.password" type="password" placeholder="登入密码"
                class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
            <input v-else v-model="inputValue.password" type="text" placeholder="登入密码"
                class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
            </div>
            <div v-else-if="showPasswordInputs" class="w-full grid justify-items-center place-items-center">
            <input v-if="inputState.password" v-model="inputValue.password" type="password" placeholder="登入密码"
                class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
            <input v-else v-model="inputValue.password" type="text" placeholder="登入密码"
                class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
            </div>
            <button v-if="showPasswordInputs || embedLogin" @click="inputState.password = !inputState.password"
                class="px-2 py-1 rounded-full bg-white hover:brightness-75 duration-200 ease-in-out flex p-auto">
                <i class="fa-duotone fa-eye-low-vision my-auto mr-2" />
                密码显示
            </button>
            <div class="w-full grid md:flex justify-items-center p-6">
                <div class="w-full flex m-2">
                    <button
                    v-if="embedLogin"
                        class="w-full bg-blue-500 text-white p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                        <i class="my-auto mx-auto fa-duotone fa-right-to-bracket fa-xl" />
                        <span class="ml-4 mx-auto font-bold">
                            登入
                        </span>
                    </button>
                    <button
                    v-else
                    @click="showPasswordInputs = true"
                        class="w-full bg-blue-500 text-white p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                        <i class="my-auto mx-auto fa-duotone fa-arrow-right fa-xl" />
                        <span class="ml-4 mx-auto font-bold">
                            下一步
                        </span>
                    </button>
                </div>
                <div class="w-full flex m-2">
                    <button
                        class="w-full bg-blue-200 text-blue-500 p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                        <i class="my-auto mx-auto fa-brands fa-google fa-xl" />
                        <span class="ml-4 mx-auto font-bold">
                            Google
                        </span>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data: () => ({
        embedLogin: false,
        showPasswordInputs: false,
        imgBgClass: 'min-h-[100dvh] w-full grid justify-items-center place-items-center duration-500 ease-in-out bg-center bg-no-repeat bg-cover',
        blurWrapperClass: 'backdrop-blur-2xl',
        imgLinks: [
            "bg-[url('/auth/1.png')] min-h-[100dvh] w-full grid justify-items-center place-items-center duration-500 ease-in-out bg-center bg-no-repeat bg-cover ", 
            "bg-[url('/auth/2.png')] min-h-[100dvh] w-full grid justify-items-center place-items-center duration-500 ease-in-out bg-center bg-no-repeat bg-cover", 
            "bg-[url('/auth/3.png')] min-h-[100dvh] w-full grid justify-items-center place-items-center duration-500 ease-in-out bg-center bg-no-repeat bg-cover", 
            "bg-[url('/auth/4.png')] min-h-[100dvh] w-full grid justify-items-center place-items-center duration-500 ease-in-out bg-center bg-no-repeat bg-cover"
        ],
        fadeAnimate: "",
        loadImg: false,
        fadeAnimations: [
            "fade-up", 
            "fade-down", 
            "fade-left", 
            "fade-right", 
            "fade-up-right", 
            "fade-up-left", 
            "fade-down-right", 
            "fade-down-left", 
            "flip-left", 
            "flip-right", 
            "flip-up", 
            "flip-down", 
            "zoom-in-up", 
            "zoom-in-down", 
            "zoom-in-left", 
            "zoom-in-right",
            "zoom-out-up",
            "zoom-out-down",
            "zoom-out-left",
            "zoom-out-right",
        ],
        iframe: false,
        inputState: {
            password: true
        },
        inputValue: {
            username: '',
            password: ''
        }
    }),
    methods: {

    },
    mounted() {
        let queryEmbed = this.$route.query.embed;
        if (queryEmbed) {
            if (queryEmbed === '1') {
                this.embedLogin = true;
            }
        }
        document.addEventListener('contextmenu', (e) => {
            e.preventDefault();
        });
        
        let chooseBgLink = Math.floor(Math.random() * this.imgLinks.length);
        let chooseAnimate = Math.floor(Math.random() * this.fadeAnimations.length);
        this.imgBgClass = this.imgLinks[chooseBgLink];
        this.fadeAnimate = this.fadeAnimations[chooseAnimate];
        this.loadImg = true;
        setTimeout(() => {
            this.blurWrapperClass = 'backdrop-blur-0';
        }, 500);
        
    },
    beforeRouteLeave() {
        document.removeEventListener('contextmenu', (e) => {
            e.preventDefault();
        });
        document.querySelector('.scrollable').removeEventListener('wheel', this.preventScroll);
        document.querySelector('.scrollable').removeEventListener('touchmove', this.preventScroll);
        document.body.style.overflow = 'auto';
    },
    beforeUnmount() {
        document.removeEventListener('contextmenu', (e) => {
            e.preventDefault();
        });
        document.querySelector('.scrollable').removeEventListener('wheel', this.preventScroll);
        document.querySelector('.scrollable').removeEventListener('touchmove', this.preventScroll);
        document.body.style.overflow = 'auto';
    }
}
</script>