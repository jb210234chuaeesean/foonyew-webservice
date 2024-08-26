<template>
  <div :class="`${colorClass} ${componentClass}`">
    <slot/>
  </div>
</template>

<script>
export default {
  props: ['color-theme', 'content-class'],
  data: () => ({
    colorList: {
      red: "bg-red-100",
      orange: "bg-orange-100",
      yellow: "bg-yellow-100",
      green: "bg-green-100",
      blue: "bg-blue-100",
      indigo: "bg-indigo-100",
      purple: "bg-purple-100",
      pink: "bg-pink-100",
      rose: "bg-rose-100",
      lime: "bg-lime-100",
      emerald: "bg-emerald-100",
      teal: "bg-teal-100",
      cyan: "bg-cyan-100",
      sky: "bg-sky-100",
      fuchsia: "bg-fuchsia-100",
      violet: "bg-violet-100",
    },
  }),
  computed: {
    colorClass() {
      return this.colorList[this.colorTheme];
    },
    componentClass() {
      return this.contentClass;
    }
  },
}
</script>