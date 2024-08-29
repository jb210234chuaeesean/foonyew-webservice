<template>
    <div class="scrollable h-full w-full grid justify-items-center place-items-center bg-fixed bg-no-repeat bg-cover bg-[url('/gradientBG.png')]">
        <div class="fixed top-0 h-20 grid grid-cols-2 w-full justify-items-center place-items-center z-30 backdrop-blur-2xl">
            <div class="w-full grid justify-items-start px-4 place-items-center">
                <img src="/logo/foonyewicon.png" class="w-24">
            </div>
            <div class="w-full grid justify-items-end px-4 place-items-center">
                <button>
                    简体中文
                </button>
            </div>
        </div>
        <div class="scrollable w-full h-[70dvh] md:h-[100dvh] grid justify-items-center place-items-center backdrop-brightness-110 backdrop-blur-2xl">
            <div class="w-full grid justify-items-start px-4 md:px-0 md:justify-items-center place-items-center space-y-4">
                <h1 class="text-4xl md:text-6xl font-bold">一个<span id="text-bg-clip" class="zhHans-bold font-normal">通行证</span>管理</h1>
                <h1 class="text-4xl md:text-6xl font-bold">您在<span class="border-b-solid border-b-2 border-b-black zhHans-bold font-normal">宽柔中学</span>的<span class="rounded-full px-2 border-solid border-2 border-black zhHans-bold font-normal">一切</span></h1>
                <div class="w-full min-h-[2dvh]" />
                <button @click="dialog = true" class="bg-blue-500 text-white p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                    <i class="my-auto mx-auto fa-duotone fa-right-to-bracket fa-xl" />
                    <span class="ml-4 mx-auto font-bold">
                        立即登入
                    </span>
                </button>
            </div>
        </div>
        <div class="pb-24 w-full grid grid-cols-1 md:grid-cols-3 justify-items-center place-items-center backdrop-blur-2xl backdrop-brightness-110">
            <div class="col-span-1 md:col-span-3 p-4 w-full text-center">
                <h1 class="text-4xl font-bold">适用于校园所有身份</h1>
            </div>
            <div class="h-full w-full p-4" v-for="sec in informationCardDetails" :key="sec.id">
                <div class="h-full border border-solid rounded-2xl bg-white grid justify-items-start place-items-center p-8 hover:bg-blue-50 hover:shadow-2xl duration-200 ease-in-out">
                    <i :class="sec.icon" class="text-blue-500 fa-3x mb-4"/>
                    <h1 v-text="sec.title" class="text-blue-500 text-4xl font-bold" />
                    <p v-text="sec.content" class="text-gray-500 text-sm" />
                </div>
            </div>
        </div>
        <logindialog :show-dialog="dialog" @close-dialog="dialog = false" />
    </div>
</template>

<script>
import logindialog from '~/components/logindialog.vue';
export default {
    components: {
        logindialog
    },
    data: () => ({
        dialog: false,
        informationCardDetails: [
            {
                icon: "fa-duotone fa-user-graduate",
                title: "学生",
                content: "查询自身的出缺席、迟到记录、学业、杂费缴交情况等个人详情。",
            },
            {
                icon: "fa-duotone fa-chalkboard-user",
                title: "教职人员",
                content: "处理学生出缺席、迟到记录、填写学生成绩等。",
            },
            {
                icon: "fa-duotone fa-chart-network",
                title: "联课顾问",
                content: "处理学生的联课分数。"
            }
        ]
    }),
    methods: {
        
    },
}
</script>

<style>
#text-bg-clip {
    background: linear-gradient(90deg, #3b82f6 0%, #818cf8 35%, #FFC0CB 70%);
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    background-position: 0% 50%;
}
</style>