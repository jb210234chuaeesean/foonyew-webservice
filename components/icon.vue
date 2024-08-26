<template>
  <div>
    <i :class="`${colorClass} ${componentIcon}`" />
  </div>
</template>

<script>
export default {
  props: ['color-theme', 'content-icon'],
  data: () => ({
    colorList: {
      red: "text-red-500",
      orange: "text-orange-500",
      yellow: "text-yellow-500",
      green: "text-green-500",
      blue: "text-blue-500",
      indigo: "text-indigo-500",
      purple: "text-purple-500",
      pink: "text-pink-500",
      rose: "text-rose-500",
      lime: "text-lime-500",
      emerald: "text-emerald-500",
      teal: "text-teal-500",
      cyan: "text-cyan-500",
      sky: "text-sky-500",
      fuchsia: "text-fuchsia-500",
      violet: "text-violet-500",
    },
  }),
  computed: {
    colorClass() {
      return this.colorList[this.colorTheme];
    },
    componentIcon () {
      return this.contentIcon;
    }
  },
}
</script>