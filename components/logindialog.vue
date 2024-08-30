<template>
    <Transition name="fade">
        <div @click="exit"
            class="activatedScroll fixed top-0 min-h-screen backdrop-brightness-75 grid grid-cols-1 md:grid-cols-4 w-full z-30 overflow-y-scroll"
            v-show="dialogView">
            <div />
            <Transition name="slide-fade">
                <div class="col-span-2 w-full overflow-y-scroll h-[100dvh] md:h-full grid justify-items-center place-items-end md:place-items-center"
                    v-show="dialogView">
                    <div @click.stop
                        class="md:mt-0 mt-[20dvh] h-max md:h-fit w-full flex justify-items-center bg-gray-100 rounded-t-2xl md:rounded-2xl px-8">
                        <div class="w-full h-[80dvh] md:h-full grid justify-items-center place-items-center">
                            <div class="w-full px-4 grid grid-cols-2 pt-2">
                                <div class="w-full flex">
                                    <button
                                        class="px-2 bg-gray-200 hover:brightness-95 active:scale-95 rounded-full duration-200 ease-in-out">
                                        <i class="fa-duotone fa-window-maximize px-2 py-2 fa-md" />
                                        <span class="ml-2 font-bold text-sm">
                                            全屏展示
                                        </span>
                                    </button>
                                </div>
                                <div class="w-full flex">
                                    <button @click.stop="exit"
                                        class="ml-auto rounded-2xl bg-gray-200 hover:brightness-75 active:scale-95 duration-200 ease-in-out">
                                        <i class="fas fa-xmark fa-xl px-2" />
                                    </button>
                                </div>
                            </div>
                            <div class="activatedScroll h-full w-full grid justify-items-center place-items-center overflow-y-scroll">
                            <img src="/logo/foonyew.png" class="w-40">
                            <h1 class="mt-3 text-3xl zhHans-bold">登入</h1>
                            <div class="w-full grid justify-items-center py-2 px-4 space-y-8">
                                <input v-model="inputValue.username" placeholder="用户名/电子邮件"
                                    class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
                                <input v-if="inputState.password" v-model="inputValue.password" type="password" placeholder="登入密码"
                                    class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
                                <input v-else v-model="inputValue.password" type="text" placeholder="登入密码"
                                    class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
                                <button @click="inputState.password = !inputState.password" class="px-2 py-1 rounded-full bg-white hover:brightness-75 duration-200 ease-in-out flex p-auto">
                                    <i class="fa-duotone fa-eye-low-vision my-auto mr-2"/>
                                    密码显示
                                </button>
                            </div>
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
                    </div>
                </div>
            </Transition>
            <div />
        </div>
    </Transition>
</template>

<script>
export default {
    props: ['show-dialog'],
    computed: {
        dialogView() {
            return this.showDialog;
        }
    },
    data: () => ({
       inputState: {
            password: true
       },
       inputValue: {
            username: '',
            password: ''
       }
    }),
    watch: {
        dialogView() {
            if (this.dialogView === true) {
                document.querySelector('.scrollable').addEventListener('wheel', this.preventScroll);
                document.querySelector('.scrollable').addEventListener('touchmove', this.preventScroll);
                document.body.style.overflow = 'hidden';
                document.querySelector('.activatedScroll').addEventListener('wheel', this.enableScroll);
                document.querySelector('.activatedScroll').addEventListener('touchmove', this.enableScroll);

            }
            else {
                document.querySelector('.scrollable').removeEventListener('wheel', this.preventScroll);
                document.querySelector('.scrollable').removeEventListener('touchmove', this.preventScroll);
                document.body.style.overflow = 'auto';
                document.querySelector('.activatedScroll').removeEventListener('wheel', this.enableScroll);
                document.querySelector('.activatedScroll').removeEventListener('touchmove', this.enableScroll);
            }
        }
    },
    methods: {
        preventScroll(e) {
            e.preventDefault()
            e.stopPropagation();

            return false;
        },
        enableScroll(e) {
            e.stopPropagation();
        },
        exit() {
            this.$emit('close-dialog');
        },
    },
    beforeUnmount() {
        document.querySelector('scrollable').removeEventListener('touchmove', this.preventScroll);
        document.querySelector('scrollable').removeEventListener('wheel', this.preventScroll);
        document.querySelector('.activatedScroll').removeEventListener('wheel', this.enableScroll);
        document.querySelector('.activatedScroll').removeEventListener('touchmove', this.enableScroll);
    }
}
</script>

<style scoped>
.slide-fade-enter-active,
.slide-fade-leave-active {
    transition: all 0.3s ease;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
    opacity: 0;
    transform: translateY(-10px);
    transition: all 0.3s ease;
}

@media screen and (max-width: 768px) {

    .slide-fade-enter-active,
    .slide-fade-leave-active {
        transition: all 0.4s ease;
    }

    .slide-fade-enter-from {
        opacity: 0;
        transform: translateY(80dvh);
        transition: all 0.4s ease-out;
    }

    .slide-fade-leave-to {
        opacity: 0;
        transform: translateY(80dvh);
        transition: all 0.4s ease-in-out;
    }
}

.fade-enter-active {
    transition: opacity 0.25s;
}

.fade-leave-active {
    transition: opacity 0.25s;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>