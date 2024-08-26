<template>
  <background :color-theme="paletteColorName">
    <div class="w-[95dvw] grid grid-cols-5 justify-items-center place-items-center px-4">
      <buttonsecondary :content-class="`w-full col-span-2 grid justify-items-center place-items-center hover:backdrop-brightness-105 hover:brightness-105 hover:scale-105 active:scale-100 active:brightness-75 duration-200 ease-in-out`" :color-theme="paletteColorName">
        <span class="w-full grid justify-items-center place-items-center px-4 py-4">
          <span class="w-full grid justify-items-center place-items-center">
            <icon content-icon="fa-duotone fa-eye fa-3x" :color-theme="paletteColorName"/>
            <h1 class="pt-2 text-xl">查看最新成绩</h1>
          </span>
        </span>
      </buttonsecondary>
    </div>
  </background>
</template>

<script>
import background from "~/components/background.vue";
export default {
  components: {
    background,
  },
  data: () => ({
    paletteColorName: ""
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