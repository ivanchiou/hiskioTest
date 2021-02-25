<template>
    <ul v-if="courses && courses.length > 0" class="text-left mt-14 mx-auto md:flex md:items-start md:justify-start md:flex-wrap">
        <li v-for="course in courses" v-bind:key="course.id" class="md:w-2/6 md:inline-block">
            <div class="relative">
            <img :src="course.image" />
            <svg v-on:click="addToCart(course)" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="shopping-cart" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512" class="text-gray-300 w-5 mx-2 my-2 absolute right-0 bottom-0 cursor-pointer"><path fill="currentColor" d="M528.12 301.319l47.273-208C578.806 78.301 567.391 64 551.99 64H159.208l-9.166-44.81C147.758 8.021 137.93 0 126.529 0H24C10.745 0 0 10.745 0 24v16c0 13.255 10.745 24 24 24h69.883l70.248 343.435C147.325 417.1 136 435.222 136 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-15.674-6.447-29.835-16.824-40h209.647C430.447 426.165 424 440.326 424 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-22.172-12.888-41.332-31.579-50.405l5.517-24.276c3.413-15.018-8.002-29.319-23.403-29.319H218.117l-6.545-32h293.145c11.206 0 20.92-7.754 23.403-18.681z" class=""></path></svg>
            </div>
            <p>{{course.headline}}</p>
        </li>
    </ul>
</template>

<script>
export default {
  data() {
    return {
      courses: null
    }
  },
  created() {
    this.$nuxt.$on('get-courses', (data) => {
      this.courses = data
    })
  },
  beforeDestroy(){
    this.$nuxt.$off('get-courses')
  },
  methods: {
      addToCart(data) {
          console.log(data)
          this.$nuxt.$emit('add-to-cart', data)
      }
  }
}
</script>

<style>
</style>