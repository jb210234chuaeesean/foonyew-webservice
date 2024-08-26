<template>
  <div class="w-full grid justify-items-center place-items-center">
    <a :href="componentHref" :class="`${colorClass} ${componentClass}`" :target="componentTarget">
      <slot/>
    </a>
  </div>
</template>

<script>
export default {
  props: ['color-theme', 'content-class', 'content-href', 'content-target'],
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
  computed: {
    colorClass() {
      return this.colorList[this.colorTheme];
    },
    componentClass() {
      return this.contentClass;
    },
    componentHref() {
      return this.contentHref;
    },
    componentTarget() {
      return this.contentTarget;
    },
  },
}
</script>