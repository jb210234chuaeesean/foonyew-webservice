<template>
    <Transition name="fade">
    <div @click="exit" class="fixed top-0 min-h-screen backdrop-brightness-75 grid grid-cols-1 md:grid-cols-4 w-full z-30" v-show="dialogView">
        <div />
        <Transition name="slide-fade">
        <div class="w-full h-full col-span-1 md:col-span-2 grid justify-items-center place-items-end md:place-items-center" v-show="dialogView">
            <div class="md:mt-0 mt-[50dvh] h-[50dvh] md:h-fit col-span-2 w-full grid justify-items-center bg-gray-100 rounded-t-2xl md:rounded-2xl p-8">
                <div class="w-full grid justify-items-start place-items-center">
                    <h1 class="text-2xl font-bold">登入</h1>
                </div>
                <div class="w-full grid justify-items-end place-items-center">

                </div>
                <div class="col-span-2 w-full grid justify-items-center px-12">
                    <button class="bg-blue-500 text-white p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                    <i class="my-auto mx-auto fa-brands fa-google fa-xl" />
                    <span class="ml-4 mx-auto font-bold">
                        使用Google登入
                    </span>
                </button>
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
    watch: {
        dialogView() {
            if (this.dialogView === true) {
        document.querySelector('.scrollable').addEventListener('wheel', this.preventScroll);
        document.querySelector('.scrollable').addEventListener('touchmove', this.preventScroll);
      }
      else {
        document.querySelector('.scrollable').removeEventListener('wheel', this.preventScroll);
        document.querySelector('.scrollable').removeEventListener('touchmove', this.preventScroll);
      }
        }
    },
    methods: {
        preventScroll(e) {
            e.preventDefault()
            e.stopPropagation();

            return false;
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

.fade-enter-from, .fade-leave-to {
    opacity: 0;
}
</style>