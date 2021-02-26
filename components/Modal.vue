<template>
    <div v-if="isOpen" class="main-modal fixed z-10 inset-0 overflow-y-auto">
        <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
            <div class="fixed inset-0 transition-opacity" aria-hidden="true">
                <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
            </div>
            <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>
            <div class="inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full" role="dialog" aria-modal="true" aria-labelledby="modal-headline">
                <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
                    <div class="bg-layout">
                        <div class="flex justify-end" >
                            <svg aria-hidden="true" v-on:click="modalClose" focusable="false" data-prefix="fas" data-icon="times" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 352 512" class="text-gray-500 w-4 mx-2 my-2 inline cursor-pointer"><path fill="currentColor" d="M242.72 256l100.07-100.07c12.28-12.28 12.28-32.19 0-44.48l-22.24-22.24c-12.28-12.28-32.19-12.28-44.48 0L176 189.28 75.93 89.21c-12.28-12.28-32.19-12.28-44.48 0L9.21 111.45c-12.28 12.28-12.28 32.19 0 44.48L109.28 256 9.21 356.07c-12.28 12.28-12.28 32.19 0 44.48l22.24 22.24c12.28 12.28 32.2 12.28 44.48 0L176 322.72l100.07 100.07c12.28 12.28 32.2 12.28 44.48 0l22.24-22.24c12.28-12.28 12.28-32.19 0-44.48L242.72 256z" class=""></path>
                            </svg>
                        </div>
                        <Logo style="width: 140px; height: 20px;" />
                        <header class="w-full overflow-hidden my-8">
                            <div class="flex justify-center">
                                <a class="btn float-left active text-4xl text-tiffanyblue font-black">登入</a>
                            </div>
                            <div class="mx-auto clear-both bg-white">
                                <span class="mx-auto mt-4 border-t-4 w-20 border-tiffanyblue block"></span>
                            </div>
                        </header>
                         <form v-on:submit.prevent="login" class="w-full p-4 flex flex-col bg-white">
                            <p class="text-center text-gray-700 text-xl mt-6 mb-6">使用 HiSKIO ID 登入
                            </p>
                            <div class="mx-auto overflow-hidden w-320px flex justify-center">
                                <ul>
                                    <li class="relative mb-4">
                                        <p class="text-hi-input-error-red text-xs error-msg" style="display: none;">
                                        </p>
                                        <div class="relative text-gray-600 focus-within:text-gray-400">
                                            <span class="absolute inset-y-0 left-0 flex items-center pl-2">
                                                <div class="p-1 focus:outline-none focus:shadow-outline">
                                                    <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="user-circle" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 496 512" class="text-gray-400 w-5 mx-2 my-2 inline"><path fill="currentColor" d="M248 8C111 8 0 119 0 256s111 248 248 248 248-111 248-248S385 8 248 8zm0 96c48.6 0 88 39.4 88 88s-39.4 88-88 88-88-39.4-88-88 39.4-88 88-88zm0 344c-58.7 0-111.3-26.6-146.5-68.2 18.8-35.4 55.6-59.8 98.5-59.8 2.4 0 4.8.4 7.1 1.1 13 4.2 26.6 6.9 40.9 6.9 14.3 0 28-2.7 40.9-6.9 2.3-.7 4.7-1.1 7.1-1.1 42.9 0 79.7 24.4 98.5 59.8C359.3 421.4 306.7 448 248 448z" class=""></path></svg>
                                                </div>
                                            </span>
                                            <input type="text" ref="account" placeholder="請輸入 HiSKIO ID" name="account" id="account" v-model="account" class="py-2 text-base text-black bg-gray-200 rounded-md pl-14 focus:outline-none focus:text-gray-900" autocomplete="off">
                                        </div>
                                    </li>
                                    <li class="relative ">
                                        <p class="text-hi-input-error-red text-xs error-msg" style="display: none;">
                                        </p>
                                        <div class="relative text-gray-600 focus-within:text-gray-400">
                                            <span class="absolute inset-y-0 left-0 flex items-center pl-2">
                                                <div class="p-1 focus:outline-none focus:shadow-outline">
                                                    <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="lock" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="text-gray-400 w-5 mx-2 my-2 inline"><path fill="currentColor" d="M400 224h-24v-72C376 68.2 307.8 0 224 0S72 68.2 72 152v72H48c-26.5 0-48 21.5-48 48v192c0 26.5 21.5 48 48 48h352c26.5 0 48-21.5 48-48V272c0-26.5-21.5-48-48-48zm-104 0H152v-72c0-39.7 32.3-72 72-72s72 32.3 72 72v72z" class=""></path></svg>
                                                </div>
                                            </span>
                                            <input type="password" v-model="password" placeholder="請輸入登入密碼" name="password" id="password" class="py-2 text-base text-black bg-gray-200 rounded-md pl-14 focus:outline-none focus:text-gray-900" autocomplete="off">
                                        </div>
                                    </li>
                                </ul>
                            </div>
                            <div class="policy text-center">
                                <label class="inline-flex items-center mt-3">
                                    <input type="checkbox" class="form-checkbox h-5 w-5 text-tiffanyblue" v-model="checked">
                                    <span class="ml-2 text-gray-700">
                                       <p class="text-gray-500 text-sm md:text-base">登入註冊即代表您同意<a href="https://hiskio.com/user-policy" target="_blank" class="underline cursor-pointer">使用者</a>及<a  href="https://hiskio.com/privacy-policy" target="_blank" class="underline cursor-pointer">隱私權政策</a></p>
                                    </span>
                                </label>
                            </div>
                            <a class="submitbtn"></a> 
                            <input type="submit" value="登入" class="mt-3 w-full inline-flex justify-center rounded-md border border-tiffanyblue px-4 py-2 bg-tiffanyblue text-base font-medium text-white hover:bg-gray-50 hover:text-tiffanyblue focus:outline-none" />
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    props: ['isInitialOpen','closeFunc'],
    data: function () {
        return {
            isOpen: this.isInitialOpen,
            focus: false,
            account: "",
            password: "",
            checked: true
        }
    },
    updated: function () {
        this.$nextTick(function () {
            if (this.isOpen && this.focus) {
                this.focusInput();
                this.focus = false
            }
        })
    },
    watch: {
        isInitialOpen: {
            handler: function (val, oldVal) {
                if(val != oldVal) {
                    this.focus = true
                }
                this.isOpen = val;
            },
            immediate: true
        },
    },    
    methods: {
        focusInput() {
            this.$refs.account.focus();
        },      
        modalClose: function () {      
            if(this.closeFunc && typeof this.closeFunc === 'function') {
                this.closeFunc();
            } else {
                this.isOpen = false;
            }
        },
        login: function() {
            const account = this.account
            const password = this.password
            if(account && password && this.checked) {
                $nuxt.$loading.start()
                axios
                    .post('https://api.hiskio.com/v2/auth/login', {
                        account,
                        password
                    })
                    .then(response => {
                        if(response.status === 200 || response.status === 202) {
                            this.modalClose();
                            $nuxt.$emit('update-is-login', true)
                            axios
                                .get('https://api.hiskio.com/v2/courses/fundraising', {
                                })
                                .then(response => {
                                    $nuxt.$emit('get-courses', response.data)
                                }).finally( function() {
                                    $nuxt.$loading.finish()
                                })
                        } else {
                            alert("帳號或密碼錯誤")
                        }
                    }).catch(
                        function (error) {
                            alert("帳號或密碼錯誤")
                            console.log('Error', error.message);
                        }
                    )
            } else {
                alert("請輸入帳號與密碼與同意隱私權政策")
            }
        }
    }
}
</script>

<style>
</style>
