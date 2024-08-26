<template>
  <background :color-theme="paletteColorName">
    <div class="w-[95dvw] grid justify-items-center place-items-center">
      <bgsecondary content-class="rounded-3xl w-full h-full grid justify-items-center place-items-center py-4"
                   :color-theme="paletteColorName">
        <div class="px-4 w-full h-full grid grid-cols-2 justify-items-center place-items-center">
          <div class="w-full h-full grid justify-items-start place-items-center">
            <h1 class="text-2xl">缺席/请假记录</h1>
          </div>
          <div class="w-full h-full grid justify-items-end place-items-center">
            <inputsecondary :color-theme="paletteColorName"
                            :content-class="`px-3 py-3 outline-none rounded-full w-full brightness-95 hover:brightness-90 focus:scale-105 duration-200 ease-in-out border-none focus:border-solid border border-black`"
                            content-placeholder="搜索……"/>
          </div>
        </div>
        <div class="w-full grid-cols-7 py-2 grid justify-items-center place-items-center">
          <bgtertiary v-for="head in tableHead" :key="head" :color-theme="paletteColorName"
                      content-class="py-4 w-full h-full grid justify-items-center place-items-center">
            <h1 class="text-md">{{ head }}</h1>
          </bgtertiary>
        </div>
        <div class="h-[30dvh] overflow-y-scroll w-full py-2 grid justify-items-center place-items-center">
          <div v-if="norecord" class="w-full grid justify-items-center place-items-center">
            <icon content-icon="my-4 far fa-clipboard-check fa-4x" :color-theme="paletteColorName"></icon>
            <textprimary content-class="text-2xl font-bold w-full grid justify-items-center place-items-center"
                         :color-theme="paletteColorName">
              目前没有缺席/请假记录
            </textprimary>
            <textprimary content-class="font-bold w-full grid justify-items-center place-items-center"
                         :color-theme="paletteColorName">
              若发现有未被输入系统的缺席或请假记录，请联系班导或训导处。
            </textprimary>
          </div>
          <div v-else
               class="w-full grid justify-items-center place-items-start">
            <div
                v-for="sec in records" :key="sec.id"
                class="w-full justify-items-center place-items-center">
              <button @click="viewDetailedData(sec)"
                      class="py-4 w-full grid grid-cols-7 justify-items-center place-items-center hover:backdrop-brightness-95 active:backdrop-brightness-90 duration-200 ease-in-out">
                <span>
                  {{ sec.date }}
                </span>
                <span>
                  <span v-for="subject in sec.subjects" v-text="`${subject} `"/>
                </span>
                <span>
                  <span v-for="periods in sec.periods" v-text="`${periods} `"/>
                </span>
                <span>
                  {{ sec.type }}
                </span>
                <span>
                  {{ sec.processTime }}
                </span>
                <span>
                  {{ sec.leaveLetter }}
                </span>
                <span>
                  <h1 v-if="sec.parentsInformed">已通知家长</h1>
                  <h1 v-else>--</h1>
                </span>
              </button>
              <div class="col-span-7 w-full min-h-[1pt] bg-gray-400"></div>
            </div>
          </div>
        </div>
        <div class="w-full px-4 grid justify-items-start place-items-center">
          最近更新于：{{ updatedDate }}
        </div>
      </bgsecondary>
    </div>
    <Transition name="fade">
      <div v-show="dialogView"
           class="absolute top-0 w-full h-full grid grid-cols-4 justify-items-center place-items-center backdrop-brightness-75 z-20">
        <div class="invisible"/>
        <Transition name="scale-fade">
          <bgsecondary v-show="dialogView"
                       content-class="rounded-3xl w-full grid col-span-2 justify-items-center place-items-center py-4"
                       :color-theme="paletteColorName">
            <div class="grid justify-items-center place-items-center w-full">
              <icon v-if="dialog.viewerIndex !== -1" :content-icon="`${dialog.icon} fa-3x`"/>
              <h1 class="mt-2 text-2xl font-bold" v-text="dialog.title"/>
              <p v-if="dialog.viewerIndex !== -1" v-text="dialog.content"/>
              <div class="h-[64dvh] overflow-y-scroll px-4 py-2 w-full text-lg" v-if="dialog.viewerIndex === 'info'">
                <div
                    class="grid w-full justify-items-center place-items-center">
                  <div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2 ">
                      <div>日期：</div>
                      {{ detailedInfo.date }}
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>科目：</div>
                      <div>
                        <span v-for="subject in detailedInfo.subjects" v-text="`${subject} `"/>
                      </div>
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>节次：</div>
                      <div>
                        <span v-for="periods in detailedInfo.periods" v-text="`${periods} `"/>
                      </div>
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>类型：</div>
                      {{ detailedInfo.type }}
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>处理时间：</div>
                      {{ detailedInfo.processTime }}
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>请假信：</div>
                      {{ detailedInfo.leaveLetter }}
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>通知家长/家长来电</div>
                      <div>
                        <h1 v-if="detailedInfo.parentsInformed">已通知家长</h1>
                        <h1 v-else>--</h1>
                      </div>
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>备注：</div>
                      {{ detailedInfo.note }}
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>班主任已批假：</div>
                      {{ detailedInfo.classTeacherProcessTime }}
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>处理人员邮箱：</div>
                      {{ detailedInfo.userEmailOfProcess }}
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>批假者：</div>
                      {{ detailedInfo.departmentProcessTime }}
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>提交者：</div>
                      {{ detailedInfo.submitEmail }}
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>事由：</div>
                      {{ detailedInfo.reason }}
                    </div>
                    <div class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>备注：</div>
                      {{ detailedInfo.reasonnote }}
                    </div>
                    <div v-if="detailedInfo.cocuricullarProcessTime !== undefined || detailedInfo.cocuricullarProcessTime !== null" class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>联课处理时间：</div>
                      {{ detailedInfo.cocuricullarProcessTime }}
                    </div>
                    <div v-if="detailedInfo.cocuricullarEmailOfProcess !== undefined || detailedInfo.cocuricullarEmailOfProcess !== null" class="grid-cols-2 grid justify-items-start place-items-center py-2">
                      <div>处理者：</div>
                      {{ detailedInfo.cocuricullarEmailOfProcess }}
                    </div>
                  </div>
                </div>
              </div>
              <div class="w-full grid justify-items-center place-items-center px-8 mt-4">
                <buttontertiary @click="clearDialog()"
                                content-class="ml-1 mr-1 rounded-3xl w-full py-2 hover:brightness-105 hover:scale-105 active:brightness-95 active:scale-100 duration-200 ease-in-out"
                                :color-theme="paletteColorName">
                  确定
                </buttontertiary>
              </div>
            </div>
          </bgsecondary>
        </Transition>
        <div class="invisible"/>
      </div>
    </Transition>
  </background>
</template>

<script>
import inputsecondary from "~/components/inputsecondary.vue";
import Bgtertiary from "~/components/bgtertiary.vue";
import colorDataList from "~/assets/json/colorDataList.json";
import list from "~/assets/json/colorList.json";


export default {
  components: {
    Bgtertiary,
    inputsecondary,
  },
  data: () => ({
    colorIndex: ["red", "orange", "yellow", "green", "blue", "indigo", "purple", "pink", "rose", "lime", "emerald", "teal", "cyan", "sky", "fuchsia", "violet"],
    colorList: {},
    darkColorList: {},
    paletteColorName: "",
    tableHead: ["日期", "科目", "节次", "类型", "处理时间", "请假信", "通指家长/家长来电"],
    norecord: false,
    records: [{
      date: 13 / 5,
      subjects: ["历史", "数学"],
      periods: [7, 8],
      type: "公假",
      processTime: "2023-5-13 12:00",
      leaveLetter: "联课活动处",
      parentsInformed: false,
      note: "",
      classTeacherProcessTime: "2023-5-13 12:00",
      userEmailOfProcess: "chintzetung@foonyew.edu.my",
      departmentProcessTime: "2023-5-13 12:00",
      submitEmail: "chintzetung@foonyew.edu.my",
      reason: "电脑常识比赛参加者",
      reasonnote: "",
      cocuricullarProcessTime: "2023-5-13 12:00",
      cocuricullarEmailOfProcess: "chintzetung@foonyew.edu.my"
    },
      {
        date: 13 / 5,
        subjects: ["历史", "数学"],
        periods: [7, 8],
        type: "公假",
        processTime: "2023-5-13 12:00",
        leaveLetter: "联课活动处",
        parentsInformed: false,
        note: "",
        classTeacherProcessTime: "2023-5-13 12:00",
        userEmailOfProcess: "chintzetung@foonyew.edu.my",
        departmentProcessTime: "2023-5-13 12:00",
        submitEmail: "chintzetung@foonyew.edu.my",
        reason: "电脑常识比赛参加者",
        reasonnote: "",
        cocuricullarProcessTime: "2023-5-13 12:00",
        cocuricullarEmailOfProcess: "chintzetung@foonyew.edu.my"
      },
    ],
    updatedDate: new Date().toLocaleString(),
    dialogView: false,
    dialog: {
      title: "",
      icon: "",
      content: "",
      viewerIndex: -1,
    },
    detailedInfo: {}
  }),
  methods: {
    setRandomTheme() {
      let randomThemeIndex = Math.floor(Math.random() * this.colorIndex.length);
      this.paletteColorName = this.colorIndex[randomThemeIndex];
      sessionStorage.setItem("theme", this.colorIndex[randomThemeIndex]);
    },
    viewDetailedData(item) {
      this.dialogView = true
      this.dialog = {
        title: "缺席/请假详细信息",
        icon: "",
        content: "",
        viewerIndex: "info",
      }
      this.detailedInfo = item
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
      } else {
        if (sessionGetTheme) {
          this.paletteColorName = sessionGetTheme;
        } else {
          this.setRandomTheme();
        }
      }
    } catch (error) {
      console.error(error)
    }
  }
}
</script>

<style scoped>

</style>