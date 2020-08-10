<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
import addBlog from "./components/addBlog.vue"
import showBlogs from "./components/showBlogs.vue"
export default {
  components: {
      'addBlog': addBlog,
      'show-blogs':showBlogs
    },

  data () {
    
    return {
    
    }
  },

  methods: {

  }
}
</script>

<style>
body{
  margin: 0;
  font-family: 'Nunito SemiBold';
}
</style>
