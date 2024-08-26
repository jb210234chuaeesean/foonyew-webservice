<template>
      <div class="text-white w-full px-4 py-8 grid justify-items-center place-items-center" :class="backgroundColorClass">
        <img src="/logo/foonyewicon.png" class="mb-8 w-32">
        <h1 class="text-sm">
            Copyright &copy; <a class="duration-200 ease-in-out hover:underline hover:brightness-95" href="https://foonyew.edu.my/home" target="_blank">新山宽柔中学</a> {{ new Date().getFullYear() }} · 版权所有，保留一切权利。
        </h1>
      </div>
  </template>
  
  <script>
  export default {
    props: ['color-theme'],
    data: () => ({
      colorList: {
        red: "bg-red-950",
        orange: "bg-orange-950",
        yellow: "bg-yellow-950",
        green: "bg-green-950",
        blue: "bg-blue-950",
        indigo: "bg-indigo-950",
        purple: "bg-purple-950",
        pink: "bg-pink-950",
        rose: "bg-rose-950",
        lime: "bg-lime-950",
        emerald: "bg-emerald-950",
        teal: "bg-teal-950",
        cyan: "bg-cyan-950",
        sky: "bg-sky-950",
        fuchsia: "bg-fuchsia-950",
        violet: "bg-violet-950",
      },
      bgColorList: {
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
      }
    }),
    computed: {
      backgroundColorClass() {
        if (this.colorTheme === '') {
            return 'bg-gray-800'
        }
        else {
            return this.colorList[this.colorTheme];
        }
      },
    },
  }
  </script>