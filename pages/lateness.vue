<template>
  <background :color-theme="paletteColorName">
    <div class="w-[95dvw] grid justify-items-center place-items-center">
      <bgsecondary content-class="rounded-3xl w-full h-full grid justify-items-center place-items-center py-4" :color-theme="paletteColorName">
        <div class="px-4 w-full h-full grid grid-cols-2 justify-items-center place-items-center">
          <div class="w-full h-full grid justify-items-start place-items-center">
            <h1 class="text-2xl">迟到记录</h1>
          </div>
          <div class="w-full h-full grid justify-items-end place-items-center">
            <inputsecondary :color-theme="paletteColorName" :content-class="`px-3 py-3 outline-none rounded-full w-full brightness-95 hover:brightness-90 focus:scale-105 duration-200 ease-in-out border-none focus:border-solid border border-black`" content-placeholder="搜索……" />
          </div>
        </div>
        <div class="w-full grid-cols-10 py-2 grid justify-items-center place-items-center">
          <bgtertiary v-for="head in tableHead" :key="head" :color-theme="paletteColorName" content-class="py-4 w-full h-full grid justify-items-center place-items-center">
            <h1 class="text-md">{{ head }}</h1>
          </bgtertiary>
        </div>
        <div class="h-[30dvh] overflow-y-scroll w-full py-2 grid justify-items-center place-items-center">
          <div class="w-full grid justify-items-center place-items-center">
            <icon content-icon="my-4 far fa-party-horn fa-4x" :color-theme="paletteColorName"></icon>
            <textprimary content-class="text-2xl font-bold w-full grid justify-items-center place-items-center" :color-theme="paletteColorName">
              目前没有迟到记录
            </textprimary>
            <textprimary content-class="font-bold w-full grid justify-items-center place-items-center" :color-theme="paletteColorName">
              若发现有未被输入系统的迟到记录，请联系班导或训导处。
            </textprimary>
          </div>
        </div>
        <div class="w-full px-4 grid grid-cols-2 justify-items-start place-items-center">
          <div class="w-full grid justify-items-start place-items-center">
            最近更新于：{{ updatedDate }}
          </div>
          <div class="w-full grid justify-items-end place-items-center">
            <button @click="setDialog(1)" class="grid-cols-3 grid justify-items-center place-items-center hover:backdrop-brightness-90 hover:scale-105 active:scale-100 active:backdrop-brightness-75 px-1 py-1 rounded duration-200 ease-in-out">
            <icon content-icon="fa-duotone fa-question fa-xl mr-2" />
            <div class="col-span-2">
              <h1 class="font-bold">处理时间</h1>
            </div>
            </button>
          </div>
        </div>
      </bgsecondary>
    </div>
    <Transition name="fade">
    <div v-show="dialogView" class="absolute top-0 w-full h-full grid grid-cols-3 justify-items-center place-items-center backdrop-brightness-75 z-20">
      <div class="invisible" />
      <Transition name="scale-fade">
      <bgsecondary v-show="dialogView" content-class="rounded-3xl w-full grid justify-items-center place-items-center py-4" :color-theme="paletteColorName">
        <div class="grid justify-items-center place-items-center w-full">
          <icon :content-icon="`${dialog.icon} fa-3x`" />
          <h1 class="mt-2 text-2xl font-bold" v-text="dialog.title" />
          <p v-text="dialog.content" />
          <div class="w-full grid justify-items-center place-items-center px-8 mt-4">
            <buttontertiary @click="clearDialog()" v-if="dialog.viewerIndex === 1" content-class="ml-1 mr-1 rounded-3xl w-full py-2 hover:brightness-105 hover:scale-105 active:brightness-95 active:scale-100 duration-200 ease-in-out" :color-theme="paletteColorName">
              确定
            </buttontertiary>
          </div>
        </div>
      </bgsecondary>
      </Transition>
      <div class="invisible" />
    </div>
    </Transition>
  </background>
</template>

<script>
import inputsecondary from "~/components/inputsecondary.vue";
import Bgtertiary from "~/components/bgtertiary.vue";
import icon from "~/components/icon.vue";
import textprimary from "~/components/textprimary.vue";
import Buttontertiary from "~/components/buttontertiary.vue";
import colorDataList from "~/assets/json/colorDataList.json";
import list from "~/assets/json/colorList.json";

export default {
  components: {
    Buttontertiary,
    Bgtertiary,
    inputsecondary,
    icon,
    textprimary
  },
  data: () => ({
    colorIndex: ["red", "orange", "yellow", "green", "blue", "indigo", "purple", "pink", "rose", "lime", "emerald", "teal", "cyan", "sky", "fuchsia", "violet"],
    colorList: {},
    tableHead: ["日期", "科目", "节次", "进班时间", "原因", "班导处理时间", "训导处处理时间", "迟到总次数", "缺点已记录", "布告"],
    norecord: true,
    records: [{
    }],
    paletteColorName: "",
    updatedDate: new Date().toLocaleString(),
    dialogContent: {
      1: {
        title: "处理时间",
        icon: "fa-duotone fa-question",
        content: "迟到5次并且班导或训导记缺点后才会有“处理时间”",
        viewerIndex: 1,
      }
    },
    dialogView: false,
    dialog: {
      title: "",
      icon: "",
      content: "",
      viewerIndex: -1,
    }
  }),
  methods: {
    setRandomTheme() {
      let randomThemeIndex = Math.floor(Math.random() * this.colorIndex.length);
      this.paletteColorName = this.colorIndex[randomThemeIndex];
      sessionStorage.setItem("theme", this.colorIndex[randomThemeIndex]);
    },
    setDialog(item) {
      this.dialog = this.dialogContent[item];
      this.dialogView = true
    },
    clearDialog() {
      this.dialogView = false
      setTimeout(() => {
        this.dialog = {
          title: "",
          icon: "",
          content: "",
          viewerIndex: -1,
        }
      }, 300)
    }
  },
  async mounted() {
    try {
      this.colorList = list.list;
      this.colorDataList = colorDataList.list;

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
    }
    catch (error) {
      console.error(error)
    }
  }
}
</script>

<style scoped>
.scale-fade-enter-active {
  transition: transform 0.3s ease, opacity 0.1s ease;
  opacity: 1;
}

.scale-fade-leave-active {
  transition: transform 0.3s ease, opacity 0.1s ease;
  opacity: 1;
}

.scale-fade-enter-from, .scale-fade-leave-to {
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

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

</style>