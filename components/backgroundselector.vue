<template>
  <div :class="`${colorClass} ${componentClass}`">
    <slot/>
  </div>
</template>

<script>
export default {
  props: ['color-theme', 'content-class', 'show-dialog'],
  computed: {
    dialogView() {
      return this.showDialog;
    },
    colorClass() {
      if (this.colorTheme === undefined || this.colorTheme === "" || this.colorTheme === null) {
        return "bg-white";
      }
      else {
        return this.colorList[this.colorTheme];
      }
    },
    componentClass() {
      return this.contentClass;
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
  data: () => ({
    colorList: {
      red: "bg-red-200",
      orange: "bg-orange-200",
      yellow: "bg-yellow-200",
      green: "bg-green-200",
      blue: "bg-blue-200",
      indigo: "bg-indigo-200",
      purple: "bg-purple-200",
      pink: "bg-pink-200",
      rose: "bg-rose-200",
      lime: "bg-lime-200",
      emerald: "bg-emerald-200",
      teal: "bg-teal-200",
      cyan: "bg-cyan-200",
      sky: "bg-sky-200",
      fuchsia: "bg-fuchsia-200",
      violet: "bg-violet-200",
    },
  }),
  methods: {
    preventScroll(e) {
      e.preventDefault()
      e.stopPropagation();

      return false;
    }
  },
  beforeUnmount() {
    document.querySelector('scrollable').removeEventListener('touchmove', this.preventScroll);
    document.querySelector('scrollable').removeEventListener('wheel', this.preventScroll);
  }
}
</script>