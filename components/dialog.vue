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
                                    <div class="w-full flex" />
                                    <div class="w-full flex">
                                        <button @click.stop="exit"
                                            class="ml-auto rounded-2xl group active:scale-95 duration-200 ease-in-out px-2 py-2">
                                            <i
                                                class="group-hover:opacity-75 fa-duotone fa-circle-xmark fa-xl duration-200 ease-in-out" />
                                        </button>
                                    </div>
                                </div>
                                <slot />
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
export default {
    props: ['show-dialog'],
    computed: {
        dialogView() {
            return this.showDialog;
        },
    },
    data: () => ({
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
                this.loginWindow.url = "";
                document.querySelector('.scrollable').removeEventListener('wheel', this.preventScroll);
                document.querySelector('.scrollable').removeEventListener('touchmove', this.preventScroll);
                document.body.style.overflow = 'auto';
                document.querySelector('.activatedScroll').removeEventListener('wheel', this.enableScroll);
                document.querySelector('.activatedScroll').removeEventListener('touchmove', this.enableScroll);
            }
        },
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
    },
    mounted() {
        document.addEventListener('keydown', this.exitKey);
    },
    beforeRouteLeave() {
        document.querySelector('scrollable').removeEventListener('touchmove', this.preventScroll);
        document.querySelector('scrollable').removeEventListener('wheel', this.preventScroll);
        document.querySelector('activatedScroll').removeEventListener('touchmove', this.enableScroll);
        document.querySelector('activatedScroll').removeEventListener('wheel', this.enableScroll);
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