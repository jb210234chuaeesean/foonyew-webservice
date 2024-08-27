<script setup>
const error = useError()
</script>

<template>
    <NuxtLayout>
        <div class="h-[100dvh] w-full grid justify-items-center place-items-center bg-[url('/gradientBG.png')] bg-cover px-2">
            <div v-if="error.statusCode === 404" class="w-full grid justify-items-center place-items-center">
                <h1 class="text-6xl md:text-8xl zhHans-bold">
                    4(?)4
                </h1>
                <h1 class="mt-2 text-sm font-bold opacity-75">
                    HTTP ERROR 404
                </h1>
                <h1 class="mt-2 text-xl font-bold ">
                    资讯处和电脑协会再厉害都好，找不到是真的找不到。
                </h1>
                <button @click="$router.push('/')" class="mt-4 bg-blue-500 text-white text-xl p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                    返回主页
                </button>
            </div>
            <div v-else class="w-full grid justify-items-center place-items-center">
                <h1 class="text-6xl md:text-8xl zhHans-bold">
                    Err(?)r
                </h1>
                <h1 class="mt-2 text-sm font-bold opacity-75">
                    {{ error.message }}
                </h1>
                <h1 class="mt-2 text-xl font-bold ">
                    资讯处和电脑科很厉害抓人来劳改，但是现在这个问题变成他们自己的问题了。
                </h1>
                <button @click="$router.push('/')" class="mt-4 bg-blue-500 text-white text-xl p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                    返回主页
                </button>
            </div>
        </div>
    </NuxtLayout>
</template>

<script>
export default {

}
</script>