<template>
  <background :color-theme="paletteColorName">
    <div class="w-[95dvw] pt-10 my-4 grid justify-items-center place-items-center">
      <div
          class="h-full w-full grid justify-items-center place-items-center rounded-2xl bg-[url('/FY.png')] bg-center bg-cover min-h-[60dvh] shadow-2xl">
        <div
            class="h-full w-full grid grid-cols-10 justify-items-center rounded-2xl place-items-center backdrop-brightness-50">
          <button
              class="w-full grid justify-items-start place-items-center text-white group active:scale-125 duration-100 ease-in-out">
            <i class="ml-4 fa-sharp fa-regular fa-chevron-left fa-lg"/>
          </button>
          <div class="w-full col-span-5 grid justify-items-start place-items-center">
            <h1 class="text-4xl text-white font-bold">欢迎登入！</h1>
            <p class="text-lg text-white">
              请同学们定期使用系统查看自己的出缺席记录，若发现资料有误，请在办公时间向训导处报备。</p>
          </div>
          <div class="w-full col-span-3 grid justify-items-end place-items-center text-white">
            <button
                class="group rounded-full px-4 py-4 border-white border border-solid font-bold hover:bg-white hover:text-black hover:scale-105 hover:shadow-2xl hover:shadow-white active:scale-95 active:brightness-75 ease-in-out duration-200">
              <span class="grid grid-cols-4">
                <span class="w-full h-full grid justify-items-center place-items-center">
                  <i class="fas fa-clipboard-list fa-xl grid group-hover:hidden"/>
                  <i class="fas fa-arrow-right fa-xl hidden group-hover:grid"/>
                </span>
                <span class="col-span-3">
                  查看出缺席记录
                </span>
              </span>
            </button>
          </div>
          <button
              class="w-full grid justify-items-end place-items-center text-white group active:scale-125 duration-100 ease-in-out">
            <i class="mr-6 fa-sharp fa-regular fa-chevron-right fa-lg"/>
          </button>
        </div>
      </div>
    </div>
    <div class="w-[90dvw] pt-10 grid grid-cols-2 justify-items-center place-items-center">
      <div class="w-full grid justify-items-start place-items-center">
        <h1 class="text-2xl">常用功能</h1>
      </div>
      <div class="w-full grid justify-items-end place-items-center">
        <button @click="linkViewList = false" v-if="linkViewList" class="px-2 py-2 hover:backdrop-brightness-95 hover:scale-105 active:backdrop-brightness-75 active:scale-100 rounded-full duration-200 ease-in-out">
          <i class="fa-duotone fa-grid-2 fa-xl mr-2" />
          使用网格视图
        </button>
        <button @click="linkViewList = true" v-else class="px-2 py-2 hover:backdrop-brightness-95 hover:scale-105 active:backdrop-brightness-75 active:scale-100 rounded-full duration-200 ease-in-out">
          <i class="fa-duotone fa-bars fa-xl mr-2" />
          使用列表视图
        </button>
      </div>
    </div>
    <div v-if="linkViewList" class="grid-rows-2 grid-cols-2 w-[95dvw] my-4 grid justify-items-center place-items-center">
      <div class="w-full px-4 grid justify-items-center place-items-center" v-for="sec in links" :key="sec.id">
      <buttonsecondary @click="$router.push(sec.link)" :content-class="`w-full rounded-3xl my-2 py-4 grid grid-cols-6 justify-items-center place-items-center duration-200 ease-in-out hover:shadow-2xl hover:brightness-105 hover:scale-[102%] active:scale-100 active:brightness-75`" :color-theme="paletteColorName">
        <span class="col-span-2 grid justify-items-center place-items-center w-full">
          <icon :color-theme="paletteColorName" :content-icon="`fa-duotone fa-3x ${sec.icon}`"/>
        </span>
        <span class="col-span-4 grid justify-items-start place-items-center w-full">
          <h1 class="text-2xl" v-text="sec.name" />
          <p class="text-sm" v-text="sec.des" />
        </span>
      </buttonsecondary>
      </div>
    </div>
    <div v-else class="w-[95dvw] my-4 grid grid-cols-4 justify-items-center place-items-center">
      <div v-for="sec in links" :key="sec.id" class="h-full mx-2">
        <buttonsecondary
            @click="$router.push(sec.link)"
            :content-class="`rounded-2xl min-h-full w-full grid justify-items-center place-items-center py-4 duration-200 ease-in-out hover:shadow-2xl hover:brightness-105 hover:scale-105 active:scale-100 active:brightness-75`"
            :color-theme="paletteColorName">
          <span class="w-full grid justify-items-center place-items-center">
            <icon :color-theme="paletteColorName" :content-icon="`fa-duotone fa-3x ${sec.icon}`"/>
          </span>
          <span class="grid justify-items-center place-items-center px-4">
            <h1 class="pt-4 text-2xl" v-text="sec.name"/>
            <p class="pt-2 text-sm brightness-90" v-text="sec.des"/>
          </span>
        </buttonsecondary>
      </div>
    </div>
    <div class="w-[90dvw] min-h-[1pt] bg-gray-300 mt-5"></div>
    <div @click="moreView = !moreView" class="cursor-pointer w-[92dvw] rounded-3xl px-2 py-2 mt-2 grid grid-cols-2 justify-items-center place-items-center hover:backdrop-brightness-90 active:backdrop-brightness-75 duration-200 ease-in-out">
      <div class="w-full grid justify-items-start place-items-center">
        <h1 class="text-2xl">相关网站</h1>
      </div>
      <div class="w-full grid justify-items-end place-items-center">
        <button v-if="moreView" class="px-2 py-2 hover:backdrop-brightness-95 hover:scale-105 active:backdrop-brightness-75 active:scale-100 rounded-full duration-200 ease-in-out">
          <i class="fas fa-chevron-up fa-xl" />
        </button>
        <button v-else>
          <i class="fas fa-chevron-down fa-xl" />
        </button>
      </div>
    </div>
    <Transition name="slide-fade">
    <div v-show="moreView" class="grid-rows-2 grid-cols-2 w-[95dvw] grid justify-items-center place-items-center">
      <div class="w-full px-4 grid justify-items-center place-items-center" v-for="sec in more" :key="sec.id">
        <hrefsecondary :content-href="sec.link" :content-class="`group w-full rounded-3xl my-2 py-4 grid grid-cols-6 justify-items-center place-items-center duration-200 ease-in-out hover:shadow-2xl hover:brightness-105 hover:scale-[102%] active:scale-100 active:brightness-75`" content-target="_blank" :color-theme="paletteColorName">
        <span class="col-span-2 grid justify-items-center place-items-center w-full">
          <icon :content-icon="`fa-sharp fa-regular fa-xl ${sec.icon}`" :color-theme="paletteColorName" />
        </span>
          <span class="col-span-3 grid justify-items-start place-items-center w-full">
          <h1 class="text-xl" v-text="sec.name" />
        </span>
          <span class="grid justify-items-center place-items-center w-full">
            <i class="group-hover:grid hidden fa-duotone fa-link-simple" />
          </span>
        </hrefsecondary>
      </div>
    </div>
    </Transition>
  </background>
</template>

<script>
import axios from "axios";
import background from "~/components/background.vue";
import Buttonsecondary from "~/components/buttonsecondary.vue";
import Hrefsecondary from "~/components/hrefsecondary.vue";

export default {
  components: {
    Hrefsecondary,
    Buttonsecondary,
    background
  },
  data: () => ({
    contentLoaded: false,
    colorIndex: ["red", "orange", "yellow", "green", "blue", "indigo", "purple", "pink", "rose", "lime", "emerald", "teal", "cyan", "sky", "fuchsia", "violet"],
    colorList: {},
    darkColorList: {},
    paletteColorName: "",
    linkViewList: false,
    moreView: true,
    links: [
      {
        name: '缺席/请假记录',
        des: '查询自己在今年内的被各部门记录和处理的缺席和请假。',
        icon: 'fa-clipboard-user',
        link: '/attendance'
      },
      {
        name: "迟到记录",
        des: "查询自己在今年内的被各部门记录和处理的迟到。",
        icon: 'fa-timer',
        link: '/lateness'
      },
      {
        name: "缴费和刷卡记录",
        des: "查看自己由事务处及其他部门记录的缴费和刷卡相关记录。",
        icon: 'fa-id-card',
        link: '/school-fees'
      },
      {
        name: "成绩查询",
        des: "查看自己由教务处及其他部门所发出的成绩表。",
        icon: 'fa-graduation-cap',
        link: '/school-results'
      }
    ],
    more: [{
      name: "新山宽柔中学官网",
      icon: "fa-globe-asia",
      link: "https://foonyew.edu.my",
      disabled: false,
    },
      {
        name: "Moodle",
        icon: "fa-graduation-cap",
        link: "https://e.foonyew.edu.my",
        disabled: false,
      },
      {
        name: "学生订书系统",
        icon: "fa-book",
        link: "https://fybooksales.foonyew.edu.my",
        disabled: true,
      },
      {
        name: "奖助学金受惠学生系统",
        icon: "fa-award",
        link: "https://sso.foonyew.edu.my:2083/?page=1",
        disabled: false,
      }
    ]
  }),
  methods: {
    setRandomTheme() {
      let randomThemeIndex = Math.floor(Math.random() * this.colorIndex.length);
      this.paletteColorName = this.colorIndex[randomThemeIndex];
      
      sessionStorage.setItem("theme", this.paletteColorName);
    },
  },
  async mounted() {
    try {
      let localGetTheme = localStorage.getItem("theme");
      let sessionGetTheme = sessionStorage.getItem("theme");
      if (localGetTheme) {
        this.paletteColorName = localGetTheme;
      }
      else {
        if (sessionGetTheme) {
          this.paletteColorName = sessionGetTheme;
        } else {
          this.setRandomTheme();
        }
      }
    } catch (e) {
      console.error(e);
    }
  },
}
</script>

<style scoped>
.slide-fade-enter-active {
  transition: transform 0.3s ease, opacity 0.1s ease, height 0.3s ease;
  opacity: 1;
  height: auto;
}

.slide-fade-leave-active {
  transition: transform 0.3s ease, opacity 0.1s ease, height 0.3s ease;
  opacity: 1;
}

.slide-fade-enter-from, .slide-fade-leave-to {
  transform: translateY(-10dvh);
  opacity: 0;
  height: 0;
}
</style>
