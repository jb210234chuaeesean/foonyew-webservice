<template>
    <div v-if="mountedState"
        class="scrollable h-full w-full grid justify-items-center place-items-center bg-fixed bg-no-repeat bg-cover bg-[url('/gradientBG.png')]">
        <div
            class="fixed top-0 h-20 grid grid-cols-2 w-full justify-items-center place-items-center z-30 backdrop-blur-2xl">
            <div class="w-full grid justify-items-start px-4 place-items-center">
                <img src="/logo/foonyewicon.png" class="w-24">
            </div>
            <div class="w-full grid justify-items-end px-4 place-items-center">
                <button>
                    简体中文
                </button>
            </div>
        </div>
        <div
            class="scrollable w-full h-[70dvh] md:h-[100dvh] grid justify-items-center place-items-center backdrop-brightness-110 backdrop-blur-2xl">
            <div
                class="w-full grid justify-items-start px-4 md:px-0 md:justify-items-center place-items-center space-y-4">
                <h1 class="text-4xl md:text-6xl font-bold">{{ pageContent.titleTopLeft }}<span id="text-bg-clip"
                        class="zhHans-bold font-normal">{{ pageContent.titleTopCenter }}</span>{{
        pageContent.titleTopRight }}</h1>
                <h1 class="text-4xl md:text-6xl font-bold">{{ pageContent.titleBottomLeft }}<span
                        class="border-b-solid border-b-2 border-b-black zhHans-bold font-normal">{{
        pageContent.titleBottomCenter }}</span>{{ pageContent.titleBottomRightO }}<span
                        class="rounded-full px-2 border-solid border-2 border-black zhHans-bold font-normal">{{
        pageContent.titleBottomRight }}</span></h1>
                <div class="w-full min-h-[2dvh]" />
                <button @click="loadLogin"
                    class="bg-blue-500 text-white p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                    <i class="my-auto mx-auto fa-duotone fa-right-to-bracket fa-xl" />
                    <span class="ml-4 mx-auto font-bold">
                        {{ pageContent.loginButton }}
                    </span>
                </button>
            </div>
        </div>
        <div
            class="pb-24 w-full grid grid-cols-1 md:grid-cols-3 justify-items-center place-items-center backdrop-blur-2xl backdrop-brightness-110">
            <div class="col-span-1 md:col-span-3 p-4 w-full text-center">
                <h1 class="text-4xl font-bold">{{ pageContent.introHeader }}</h1>
            </div>
            <div class="h-full w-full p-4" v-for="sec in pageContent.informationCardDetails" :key="sec.id">
                <div
                    class="h-full border border-solid rounded-2xl bg-white grid justify-items-start place-items-center p-8 hover:bg-blue-50 hover:shadow-2xl duration-200 ease-in-out">
                    <i :class="sec.icon" class="text-blue-500 fa-3x mb-4" />
                    <h1 v-text="sec.title" class="text-blue-500 text-4xl font-bold" />
                    <p v-text="sec.content" class="text-gray-500 text-sm" />
                </div>
            </div>
        </div>
        <logindialog :loading-dialog="status.loading" :show-dialog="dialog" @close-dialog="closeDialog"
            @complete-load="processLoaded" />
        <authloading v-if="!status.loaded && status.loading" />
    </div>
</template>

<script>
import logindialog from '~/components/logindialog.vue';
import authloading from '~/components/general/authloading.vue';
import zhcnPassport from '~/assets/lang/zh-cn/passport.json';
import enPassport from '~/assets/lang/en/passport.json';
export default {
    components: {
        logindialog,
        authloading,
    },
    data: () => ({
        mountedState: false,
        status: {
            loaded: false,
            loading: false
        },
        dialog: false,
        pageContent: {

        }
    }),
    methods: {
        loadLogin() {
            this.status.loading = true;
        },
        processLoaded() {
            this.status.loaded = true;
            this.dialog = true;
            this.status.loading = true;
        },
        closeDialog() {
            this.dialog = false;
            setTimeout(() => {
                this.status.loaded = false;
                this.status.loading = false;
            }, 100);
            setTimeout(() => {
                if (window.innerWidth > 768) {
                    this.$router.push('/script/reloadpassport')
                }
                else {
                    window.location.reload();
                }
            }, 200)
        }
    },
    mounted() {
        this.pageContent = enPassport;
        this.mountedState = true;
    }
}
</script>

<style>
#text-bg-clip {
    background: linear-gradient(90deg, #3b82f6 0%, #818cf8 35%, #FFC0CB 70%);
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    background-position: 0% 50%;
}
</style>