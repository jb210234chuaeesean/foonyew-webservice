<template>
    <div id="signInContent"
        class="h-[100dvh] w-full grid grid-cols-1 md:grid-cols-2 justify-items-center place-items-center">
        <div class="w-full hidden md:grid justify-items-center md:justify-items-start md:place-items-center p-8">

        </div>
        <div class="w-full grid justify-items-center space-y-8">
            <img src="/logo/foonyew.png" class="w-40">
            <h1 class="mt-3 text-3xl zhHans-bold">登入</h1>
            <input v-model="inputValue.username" placeholder="用户名/电子邮件"
                class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
            <input v-if="inputState.password" v-model="inputValue.password" type="password" placeholder="登入密码"
                class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
            <input v-else v-model="inputValue.password" type="text" placeholder="登入密码"
                class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
            <button @click="inputState.password = !inputState.password"
                class="px-2 py-1 rounded-full bg-white hover:brightness-75 duration-200 ease-in-out flex p-auto">
                <i class="fa-duotone fa-eye-low-vision my-auto mr-2" />
                密码显示
            </button>
            <div class="w-full grid md:flex justify-items-center p-6">
                <div class="w-full flex m-2">
                    <button
                        class="w-full bg-blue-500 text-white p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                        <i class="my-auto mx-auto fa-duotone fa-right-to-bracket fa-xl" />
                        <span class="ml-4 mx-auto font-bold">
                            登入
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
        document.addEventListener('contextmenu', (e) => {
            e.preventDefault();
        });
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