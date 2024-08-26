<template>
  <div class="min-h-[100dvh] w-full grid justify-items-center place-items-center duration-200 ease-in-out" :class="{'pb-12': $route.path === '/'}, backgroundColorClass">
    <slot/>
  </div>
</template>

<script>
export default {
  props: ['color-theme'],
  data: () => ({
    colorList: {
      red: "bg-red-50",
      orange: "bg-orange-50",
      yellow: "bg-yellow-50",
      green: "bg-green-50",
      blue: "bg-blue-50",
      indigo: "bg-indigo-50",
      purple: "bg-purple-50",
      pink: "bg-pink-50",
      rose: "bg-rose-50",
      lime: "bg-lime-50",
      emerald: "bg-emerald-50",
      teal: "bg-teal-50",
      cyan: "bg-cyan-50",
      sky: "bg-sky-50",
      fuchsia: "bg-fuchsia-50",
      violet: "bg-violet-50",
    },
  }),
  computed: {
    backgroundColorClass() {
      return this.colorList[this.colorTheme];
    }
  },
}
</script>