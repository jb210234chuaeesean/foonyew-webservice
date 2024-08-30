<template>

  <Head>
    <Meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <Link rel="stylesheet" href="https://site-assets.fontawesome.com/releases/v6.6.0/css/all.css" />
    <Link rel="stylesheet" href="https://site-assets.fontawesome.com/releases/v6.6.0/css/sharp-duotone-solid.css" />
    <Link rel="stylesheet" href="https://site-assets.fontawesome.com/releases/v6.6.0/css/sharp-thin.css" />
    <Link rel="stylesheet" href="https://site-assets.fontawesome.com/releases/v6.6.0/css/sharp-solid.css" />
    <Link rel="stylesheet" href="https://site-assets.fontawesome.com/releases/v6.6.0/css/sharp-regular.css" />
    <Link rel="stylesheet" href="https://site-assets.fontawesome.com/releases/v6.6.0/css/sharp-light.css" />
  </Head>
  <div class="scrollable h-full w-full grid justify-items-center place-items-center">
    <Transition name="fade">
      <div v-show="dialog"
        class="fixed top-0 h-[100dvh] backdrop-brightness-75 w-full grid grid-cols-3 justify-items-center place-items-center z-20">
        <div class="invisible" />
        <Transition name="scale-fade">
          <backgroundselector v-show="dialog"
            content-class="grid justify-items-center place-items-center w-full rounded-3xl"
            :color-theme="paletteColorName">
            <div class="w-full grid grid-cols-4 justify-items-center place-items-center px-4 py-4">
              <div class="w-full col-span-2 grid justify-items-start place-items-center">
                <h1 class="text-2xl font-bold">设定网页配色</h1>
              </div>
              <div class="w-full col-span-2 grid justify-items-end place-items-center">
                <button @click="dialog = false"
                  class="hover:backdrop-brightness-90 active:scale-95 active:backdrop-brightness-75 duration-200 ease-in-out">
                  <i class="fas fa-xmark px-4 py-5 fa-xl" />
                </button>
              </div>
            </div>
            <div
              class="activatedScroll w-96 grid justify-items-center place-items-center overflow-y-scroll max-h-[60dvh] rounded-2xl">
              <button @click="removeTheme(); dialog = false"
                :class="{ 'backdrop-brightness-95': paletteColorName === '' }"
                class="rounded-2xl w-full grid grid-cols-4 justify-items-center place-items-center py-4 hover:backdrop-brightness-90 active:backdrop-brightness-75 active:scale-95 duration-200 ease-in-out">
                <span class="grid justify-items-center place-items-center">
                  <i class="fa-duotone fa-palette fa-2x" />
                </span>
                <span class="grid col-span-2 justify-items-center place-items-center">
                  <h1>自动配色</h1>
                </span>
                <span class="grid justify-items-center place-items-center">
                  <i v-if="paletteColorName === ''" class="fa-duotone fa-check" />
                </span>
              </button>
              <button @click="setTheme(sec.name); dialog = false"
                :class="{ 'backdrop-brightness-95': paletteColorName === sec.name }"
                class="rounded-2xl w-full grid grid-cols-4 justify-items-center place-items-center py-4 hover:backdrop-brightness-90 active:backdrop-brightness-75 active:scale-95 duration-200 ease-in-out"
                v-for="sec in colorDataList">
                <span class="grid justify-items-center place-items-center">
                  <icon :content-icon="`fas fa-square fa-2x`" :color-theme="sec.name" />
                </span>
                <span class="grid col-span-2 justify-items-center place-items-center">
                  <h1 v-text="sec.cname" />
                </span>
                <span class="grid justify-items-center place-items-center">
                  <i v-if="paletteColorName === sec.name" :class="sec.primarytext" class="fa-duotone fa-check" />
                </span>
              </button>
            </div>
          </backgroundselector>
        </Transition>
        <div class="invisible" />
        <div class="min-h-[4dvh] col-span-3" />
      </div>
    </Transition>
    <NuxtPage />
    <nloader />
    <div v-if="!$route.path.includes('/passport') && mountedStatus"
      class="fixed top-0 w-full grid justify-items-center place-items-center z-10">
      <div
        class="fixed top-3 w-[90dvw] h-[12dvh] grid grid-cols-9 justify-items-center place-items-center rounded-full bg-white shadow-2xl z-10">
        <div class="h-full w-full grid justify-items-center place-items-center">
          <button @click="$router.push('/')" v-if="$route.fullPath !== '/'"
            class="px-2 py-2 rounded-full hover:backdrop-brightness-90 hover:scale-105 active:backdrop-brightness-75 active:scale-95 duration-200 ease-in-out">
            <i class="fa-sharp fa-regular fa-arrow-left fa-xl" />
          </button>
        </div>
        <div class="w-full col-span-3 grid justify-items-center place-items-center">
          <input
            class="ml-10 px-4 py-4 outline-none rounded-full bg-gray-200 w-full hover:brightness-90 focus:scale-105 duration-200 ease-in-out border-none focus:border-solid border border-black"
            placeholder="搜索……">
        </div>
        <div class="invisible col-span-3" />
        <div class="w-full grid justify-items-center place-items-center">
          <button @click="dialog = true"
            class="w-full px-2 py-2 rounded-full border border-solid border-black hover:backdrop-brightness-90 hover:scale-105 active:backdrop-brightness-75 active:scale-95 duration-200 ease-in-out">
            <span>
              <i class="fa-duotone fa-palette fa-xl mr-2" />
            </span>
            配色
          </button>
        </div>
      </div>
    </div>
    <layoutFooter v-if="($route.path === '/' || $route.path.includes('/passport')) && mountedStatus"
      :color-theme="paletteColorName" />
  </div>
</template>

<script>
import icon from "~/components/icon";
import backgroundselector from "~/components/backgroundselector.vue";
import layoutFooter from "./components/layout/footer.vue";
import colorDataList from "~/assets/json/colorDataList.json";
import dcolorDataList from "~/assets/json/darkColorList.json";
import list from "~/assets/json/colorList.json";
import nloader from "~/components/nprogress/loader.vue"

export default {
  components: {
    icon,
    backgroundselector,
    layoutFooter,
    nloader
  },
  data: () => ({
    mountedStatus: false,
    colorIndex: ["red", "orange", "yellow", "green", "blue", "indigo", "purple", "pink", "rose", "lime", "emerald", "teal", "cyan", "sky", "fuchsia", "violet"],
    colorDataList: [],
    colorList: {},
    darkColorList: {},
    paletteColorName: "",
    dialog: false,
    footerClass: "",
  }),
  watch: {
    dialog() {
      if (this.dialog === true) {
        document.querySelector('.scrollable').addEventListener('wheel', this.preventScroll);
        document.querySelector('.scrollable').addEventListener('touchmove', this.preventScroll);
        document.querySelector('.activatedScroll').addEventListener('wheel', this.enableScroll);
        document.querySelector('.activatedScroll').addEventListener('touchmove', this.enableScroll);
        document.body.style.overflow = 'hidden';
      }
      else {
        document.querySelector('.scrollable').removeEventListener('wheel', this.preventScroll);
        document.querySelector('.scrollable').removeEventListener('touchmove', this.preventScroll);
        document.querySelector('.activatedScroll').removeEventListener('wheel', this.enableScroll);
        document.querySelector('.activatedScroll').removeEventListener('touchmove', this.enableScroll);
        document.body.style.overflow = 'auto';
      }
    }
  },
  methods: {
    setTheme(item) {
      localStorage.setItem("theme", item);
      sessionStorage.setItem("reloadThemeRoute", this.$route.fullPath)
      this.paletteColorName = item;
      this.$router.push('/script/reloadtheme')
    },
    removeTheme() {
      localStorage.removeItem("theme");
      sessionStorage.setItem("reloadThemeRoute", this.$route.fullPath)
      this.$router.push('/script/reloadtheme')
      this.paletteColorName = "";
    },
    preventScroll(e) {
      e.preventDefault()
      e.stopPropagation();
      return false;
    },
    enableScroll(e) {
      e.stopPropagation();
    },
  },
  async mounted() {
    try {
      this.colorList = list.list;
      this.colorDataList = colorDataList.list;
      this.darkColorList = dcolorDataList;

      let localGetTheme = localStorage.getItem("theme");
      let sessionGetTheme = sessionStorage.getItem("theme");

      if (!this.$route.path.includes('/passport')) {
        if (localGetTheme) {
          this.paletteColorName = localGetTheme;
        } else {
          if (sessionGetTheme) {
            this.paletteColorName = "";
          } else {
            this.paletteColorName = "";
          }
        }
      }

      this.mountedStatus = true;
    } catch (e) {
      console.error(e);
    }
  },
}
</script>

<style>
@font-face {
  font-family: 'MiSans';
  src: url('~/assets/fonts/MiSans/MiSans-Normal.ttf') format('truetype');
}

@font-face {
  font-family: 'Gotham';
  src: url('~/assets/fonts/Gotham/GothamBook.ttf') format('truetype');
}

@font-face {
  font-family: 'Inpin';
  src: url('~/assets/fonts/Inpin/inpin.ttf') format('truetype');
}

html,
body,
img {
  font-family: 'MiSans', sans-serif;
  user-select: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-touch-callout: none;
  -webkit-tap-highlight-color: transparent;
}

::-webkit-scrollbar {
  display: none;
}

.scale-fade-enter-active {
  transition: transform 0.3s ease, opacity 0.1s ease;
  opacity: 1;
}

.scale-fade-leave-active {
  transition: transform 0.3s ease, opacity 0.1s ease;
  opacity: 1;
}

.scale-fade-enter-from,
.scale-fade-leave-to {
  transform: scale(0.9);
  opacity: 0;
}

.fade-enter-active {
  transition: opacity 0.1s ease;
  opacity: 1;
}

.fade-leave-active {
  transition: opacity 0.1s ease;
  opacity: 1;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.eng-typeface {
  font-family: 'Gotham', sans-serif;
}

.zhHans-bold {
  font-family: 'Inpin', sans-serif;
}
</style>