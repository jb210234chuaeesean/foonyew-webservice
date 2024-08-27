<template>
    <img src="/logo/foonyew.png" class="w-40">
                <h1 class="mt-3 text-3xl zhHans-bold">登入</h1>
                <div class="w-full grid justify-items-center py-2 px-4 space-y-8">
                    <input placeholder="用户名/电子邮件" class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
                    <input type="password" placeholder="登入密码" class="bg-gray-200 border-solid border-transparent border-2 focus:border-blue-500 focus:shadow-2xl focus:shadow-blue-500 focus:outline-none w-full p-4 rounded-full hover:shadow-2xl hover:border-blue-500 hover:brightness-105 duration-200 ease-in-out">
                </div>
                <div class="w-full grid md:flex justify-items-center p-6">
                    <div class="w-full flex m-2">
                    <button class="w-full bg-blue-500 text-white p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                    <i class="my-auto mx-auto fa-duotone fa-right-to-bracket fa-xl" />
                    <span class="ml-4 mx-auto font-bold">
                        登入
                    </span>
                    </button>
                    </div>
                    <div class="w-full flex m-2">
                    <button class="w-full bg-blue-200 text-blue-500 p-4 flex rounded-full hover:brightness-95 hover:scale-105 active:brightness-75 active:scale-100 duration-200 ease-in-out">
                    <i class="my-auto mx-auto fa-brands fa-google fa-xl" />
                    <span class="ml-4 mx-auto font-bold">
                        Google
                    </span>
                    </button>
                    </div>
                    </div>
</template>

<script>
export default {
    
}
</script>