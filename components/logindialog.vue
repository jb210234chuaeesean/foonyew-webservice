<template>
    <div v-if="dialogLoading" class="h-[100dvh] w-full grid justify-items-center place-items-center">
        <Transition name="fade">
            <div @click="exit"
                class="activatedScroll fixed top-0 min-h-screen backdrop-brightness-75 grid grid-cols-1 md:grid-cols-4 w-full z-30 overflow-y-scroll"
                v-show="dialogView">
                <div />
                <Transition name="slide-fade">
                    <div class="col-span-2 w-full overflow-y-scroll h-full md:h-full grid justify-items-center place-items-end md:place-items-center"
                        v-show="dialogView">
                        <div @click.stop
                            class="md:mt-0 mt-[5dvh] h-max md:h-fit w-full flex justify-items-center place-items-start bg-gray-100 rounded-t-2xl md:rounded-2xl px-8">
                            <div class="w-full h-[95dvh] md:h-full grid justify-items-center place-items-start">
                                <div class="w-full pt-2 px-4 grid grid-cols-2">
                                    <div class="w-full flex">
                                        <button @click.stop="$router.push('/auth/signin')"
                                            class="mr-auto rounded-2xl hover:opacity-75 active:scale-95 duration-200 ease-in-out bg-gray-300 px-2 py-2">
                                            <i
                                                class="fa-duotone fa-browser fa-md duration-200 ease-in-out mr-2" />
                                            在浏览器登入
                                        </button>
                                    </div>
                                    <div class="w-full flex">
                                        <button @click.stop="exit"
                                            class="ml-auto rounded-2xl group active:scale-95 duration-200 ease-in-out px-2 py-2">
                                            <i
                                                class="group-hover:opacity-75 fa-duotone fa-circle-xmark fa-xl duration-200 ease-in-out" />
                                        </button>
                                    </div>
                                </div>
                                <dynamicSignIn class="grid w-full" v-if="loginWindow.dynamicSignIn" />
                                <iframe id="loginFrame" v-else @load="frameLoaded()" class="grid w-full h-[80dvh]"
                                    :src="loginWindow.url" />
                            </div>
                        </div>
                    </div>
                </Transition>
                <div />
            </div>
        </Transition>
    </div>
</template>

<script>
import dynamicSignIn from '~/components/innercomponent/login.vue';
export default {
    props: ['show-dialog', 'loading-dialog'],
    components: {
        dynamicSignIn
    },
    computed: {
        dialogView() {
            return this.showDialog;
        },
        dialogLoading() {
            return this.loadingDialog;
        }
    },
    data: () => ({
        document: {
            height: 0,
            width: 0
        },
        loginWindow: {
            dynamicSignIn: false,
            url: ""
        }
    }),
    watch: {
        dialogView() {
            if (this.dialogView === true) {
                if (window.innerWidth > 768) {
                    document.querySelector('.scrollable').addEventListener('wheel', this.preventScroll);
                    document.querySelector('.scrollable').addEventListener('touchmove', this.preventScroll);
                    document.body.style.overflow = 'hidden';
                    document.querySelector('.activatedScroll').addEventListener('wheel', this.enableScroll);
                    document.querySelector('.activatedScroll').addEventListener('touchmove', this.enableScroll);
                }

            }
            else {
                this.loginWindow.url = "";
                document.querySelector('.scrollable').removeEventListener('wheel', this.preventScroll);
                document.querySelector('.scrollable').removeEventListener('touchmove', this.preventScroll);
                document.body.style.overflow = 'auto';
                document.querySelector('.activatedScroll').removeEventListener('wheel', this.enableScroll);
                document.querySelector('.activatedScroll').removeEventListener('touchmove', this.enableScroll);
            }
        },
        dialogLoading() {
            if (this.dialogLoading === true) {
                this.loginWindow.url = "/auth/signin?embed=1";
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
            this.dynamicSignIn = false
            this.$emit('close-dialog');
        },
        exitKey(e) {
            if (e.key === 'Escape') {
                this.exit();
            }
        },
        frameLoaded() {
            if (window.innerWidth > 768) {
                this.loginWindow.dynamicSignIn = true;
            }
            else {
                this.loginWindow.dynamicSignIn = false;
            }
            this.$emit('complete-load')
        },
    },
    mounted() {
        this.document.height = window.innerHeight;
        this.document.width = window.innerWidth;
        document.addEventListener('keydown', this.exitKey);
    },
    beforeRouteLeave() {
        document.querySelector('scrollable').removeEventListener('touchmove', this.preventScroll);
        document.querySelector('scrollable').removeEventListener('wheel', this.preventScroll);
        document.removeEventListener('keydown', this.exitKey);
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