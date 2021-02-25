<template>
    <div class="relative">
        <svg v-on:click="showCartList" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="shopping-cart" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512" :class="addedColor + ' w-5 mx-2 my-2 inline cursor-pointer'"><path fill="currentColor" d="M528.12 301.319l47.273-208C578.806 78.301 567.391 64 551.99 64H159.208l-9.166-44.81C147.758 8.021 137.93 0 126.529 0H24C10.745 0 0 10.745 0 24v16c0 13.255 10.745 24 24 24h69.883l70.248 343.435C147.325 417.1 136 435.222 136 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-15.674-6.447-29.835-16.824-40h209.647C430.447 426.165 424 440.326 424 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-22.172-12.888-41.332-31.579-50.405l5.517-24.276c3.413-15.018-8.002-29.319-23.403-29.319H218.117l-6.545-32h293.145c11.206 0 20.92-7.754 23.403-18.681z" class=""></path></svg>
        <div v-if="courses && courses.length > 0 && isClickedCart" v-click-outside="closeCartList" class="absolute -left-60 bg-white bg-layout shadow-md w-80">
            <svg v-on:click="closeCartList" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="times" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 352 512" class="absolute right-0 text-gray-500 w-4 mx-2 my-2 inline cursor-pointer"><path fill="currentColor" d="M242.72 256l100.07-100.07c12.28-12.28 12.28-32.19 0-44.48l-22.24-22.24c-12.28-12.28-32.19-12.28-44.48 0L176 189.28 75.93 89.21c-12.28-12.28-32.19-12.28-44.48 0L9.21 111.45c-12.28 12.28-12.28 32.19 0 44.48L109.28 256 9.21 356.07c-12.28 12.28-12.28 32.19 0 44.48l22.24 22.24c12.28 12.28 32.2 12.28 44.48 0L176 322.72l100.07 100.07c12.28 12.28 32.2 12.28 44.48 0l22.24-22.24c12.28-12.28 12.28-32.19 0-44.48L242.72 256z" class=""></path>
            </svg>
            <div class="w-full p-4 flex flex-col bg-white">
                <p class="text-center text-gray-700 text-xl mt-6 mb-6">購物車
                </p>
                <div class="mx-auto overflow-hidden w-320px flex justify-center">
                    <ul v-if="courses && courses.length > 0" class="text-left mx-auto">
                        <li v-for="course in courses" v-bind:key="course.id">
                            <img :src="course.image" />
                            <p>{{course.headline}}</p>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      courses: [],
      isClickedCart: false
    }
  },
  computed: {
    addedColor: function () {
      return this.courses && this.courses.length > 0 ? "text-red-300" : "text-gray-300"
    }
  },
  created() {
    this.$nuxt.$on('add-to-cart', (data) => {
        const removeItems = this.courses.filter((course)=>course.id == data.id)
        if(removeItems && removeItems.length > 0) {
            const items = removeItems.map((course)=>({"id":course.id, "coupon": ""}))
            axios
                .delete('https://api.hiskio.com/v2/carts', {items})
                .then(response => {
                    console.log(response)
                    this.courses = this.courses.filter((course)=>course.id != data.id)          
                }) 
        } else {
            const courses = [
                ...this.courses,
                data
            ]
            const items = courses.map((course)=>({"id":course.id, "coupon": ""}))
            console.log(items)
            axios
                .post('https://api.hiskio.com/v2/carts', {
                    items,
                    coupon: ""
                })
                .then(response => {
                    console.log(response.data.data)
                    this.courses = response.data.data           
                })
        }
    })
  },
  methods: {
      showCartList() {
          this.isClickedCart = !this.isClickedCart
      },
      closeCartList() {
          this.isClickedCart = false
      }
  },
  beforeDestroy(){
    this.$nuxt.$off('add-to-cart')
  }
}
</script>

<style>
</style>