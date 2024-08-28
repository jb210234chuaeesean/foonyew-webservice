<template>
    <Transition name="fade">
        <div @click="exit"
            class="fixed top-0 min-h-screen backdrop-brightness-75 grid grid-cols-1 md:grid-cols-4 w-full z-30"
            v-show="dialogView">
            <div />
            <Transition name="slide-fade">
                <div class="activatedScroll col-span-2 w-full overflow-y-scroll h-[100dvh] md:h-full grid justify-items-center place-items-end md:place-items-center"
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
                            <FYLogin class="h-full w-full overflow-y-scroll flex" />
                        </div>
                    </div>
                </div>
            </Transition>
            <div />
        </div>
    </Transition>
</template>

<script>
import FYLogin from './innercomponent/login.vue';
export default {
    props: ['show-dialog'],
    components: {
        FYLogin
    },
    computed: {
        dialogView() {
            return this.showDialog;
        }
    },
    watch: {
        dialogView() {
            if (this.dialogView === true) {
                document.querySelector('.scrollable').addEventListener('wheel', this.preventScroll);
                document.querySelector('.scrollable').addEventListener('touchmove', this.preventScroll);
                document.querySelector('.activatedScroll').addEventListener('wheel', this.enableScroll);
                document.querySelector('.activatedScroll').addEventListener('touchmove', this.enableScroll);

            }
            else {
                document.querySelector('.scrollable').removeEventListener('wheel', this.preventScroll);
                document.querySelector('.scrollable').removeEventListener('touchmove', this.preventScroll);
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
        }
    },
    beforeUnmount() {
        document.querySelector('scrollable').removeEventListener('touchmove', this.preventScroll);
        document.querySelector('scrollable').removeEventListener('wheel', this.preventScroll);
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