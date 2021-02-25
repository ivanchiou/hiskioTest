<template>
  <div>
    <header class="fixed top-0 z-10 w-full bg-white shadow-sm h-50px">
        <div class="flex items-center justify-between h-full mx-auto max-w-screen-lg">
        <div class="header-bar w-2/6">
            <Logo class="mx-2" />
        </div>
        <div class="flexRight">
            <span v-if="!isLogined" class="text-gray-700 transition-color textBtn hover:text-hi-more-green mx-2 my-2 block">
              我想開課
            </span>
            <span v-if="isLogined" class="text-gray-700 transition-color textBtn hover:text-hi-more-green mx-2 my-2 block">
              任務板
            </span>
            <span v-if="isLogined" class="text-gray-700 transition-color textBtn hover:text-hi-more-green mx-2 my-2 block">
              我的課程
            </span>            
            <Cart />
            <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="question-circle" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="text-gray-300 w-5 mx-2 my-2 hidden md:inline"><path fill="currentColor" d="M504 256c0 136.997-111.043 248-248 248S8 392.997 8 256C8 119.083 119.043 8 256 8s248 111.083 248 248zM262.655 90c-54.497 0-89.255 22.957-116.549 63.758-3.536 5.286-2.353 12.415 2.715 16.258l34.699 26.31c5.205 3.947 12.621 3.008 16.665-2.122 17.864-22.658 30.113-35.797 57.303-35.797 20.429 0 45.698 13.148 45.698 32.958 0 14.976-12.363 22.667-32.534 33.976C247.128 238.528 216 254.941 216 296v4c0 6.627 5.373 12 12 12h56c6.627 0 12-5.373 12-12v-1.333c0-28.462 83.186-29.647 83.186-106.667 0-58.002-60.165-102-116.531-102zM256 338c-25.365 0-46 20.635-46 46 0 25.364 20.635 46 46 46s46-20.636 46-46c0-25.365-20.635-46-46-46z" class=""></path></svg>
            <svg v-if="!isLogined" v-on:click="openModal" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="user-circle" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 496 512" class="text-gray-300 w-5 mx-2 my-2 inline cursor-pointer block md:hidden"><path data-v-12a78183="" fill="currentColor" d="M248 8C111 8 0 119 0 256s111 248 248 248 248-111 248-248S385 8 248 8zm0 96c48.6 0 88 39.4 88 88s-39.4 88-88 88-88-39.4-88-88 39.4-88 88-88zm0 344c-58.7 0-111.3-26.6-146.5-68.2 18.8-35.4 55.6-59.8 98.5-59.8 2.4 0 4.8.4 7.1 1.1 13 4.2 26.6 6.9 40.9 6.9 14.3 0 28-2.7 40.9-6.9 2.3-.7 4.7-1.1 7.1-1.1 42.9 0 79.7 24.4 98.5 59.8C359.3 421.4 306.7 448 248 448z"></path></svg>
            <img v-if="isLogined" class="w-8 h-8 rounded-full mx-2" src="https://thumbnails.f5ezcode.in/eyJidWNrZXQiOiJjZG4uaGlza2lvLmNvbSIsImtleSI6InVzZXJzXC9PTTJoVUNMOWZEMHNiRlE3LnBuZyIsImVkaXRzIjp7InBuZyI6eyJxdWFsaXR5Ijo4MH19fQ==" alt="">
            <button v-if="!isLogined" v-on:click="openModal" type="button" class="mt-3 w-full inline-flex justify-center rounded-md border border-tiffanyblue px-4 py-2 bg-white text-base font-medium text-tiffanyblue hover:bg-gray-50 focus:outline-none sm:mt-0 sm:ml-3 sm:w-auto sm:text-sm hidden md:block">
            登入
            </button>
            <button v-if="!isLogined" type="button" class="mt-3 w-full inline-flex justify-center rounded-md border border-tiffanyblue px-4 py-2 bg-tiffanyblue text-base font-medium text-white hover:bg-gray-50 hover:text-tiffanyblue focus:outline-none sm:mt-0 sm:ml-3 sm:w-auto sm:text-sm hidden md:block">
            註冊
            </button>   
        </div>
        </div>
    </header>
    <Modal v-bind:isInitialOpen="isOpenModal" v-bind:closeFunc="closeModal"/>
  </div>
</template>

<script>
export default {
    data: function () {
        return {
          isOpenModal: false,
          isLogined: false
        }
    },
    created() {
      this.$nuxt.$on('update-is-login', (value) => {
        this.isLogined = value
      })
    },
    beforeDestroy(){
      this.$nuxt.$off('update-is-login')
    },    
    methods: {
        openModal: function () {
            this.isOpenModal = true
        },
        closeModal: function (){
            this.isOpenModal = false
        }
    }
}
</script>

<style>
.h-50px {
  height: 50px;
}

.header-bar {
  height: 100%;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}

.flexRight {
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
</style>
