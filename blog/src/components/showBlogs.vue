<template>
  <div v-theme:column="'narrow'" id="show-blogs">
    <h1>All Blog Articles</h1>
    <input type="text" v-model="search" placeholder="search blogs"/>

    <div v-for="blog in filteredBlogs" :key="blog" class="single-blog">
        <router-link v-bind:to="'/blog/' + blog.id"><h2>{{ blog.title | to-uppercase }}</h2></router-link>
        <article>{{ blog.content | snippet }}</article>
    </div>
  </div>
</template>

<script>

export default {


  data () {
    return {
        blogs:[],
        search:'',
    }
  },

  methods: {

  },


  created(){
      this.$http.get('https://arched-glow-257422.firebaseio.com/posts.json').then(function(data){
        return (data.json());   
      }).then(function(data){
          var blogsArray = [];
          for(let key in data){
              data[key].id = key;
              blogsArray.push(data[key]);
          }
        
          this.blogs = blogsArray;
      })

  },

  computed:{
      filteredBlogs: function(){
          return this.blogs.filter(blog => {
              return blog.title.match(this.search.toUpperCase());
          });
      }
  },

  filters: {
      toUppercase(value){
          return value.toUpperCase();
      }
  },

  directives:{
      'rainbow':{
           bind(el, binding, vnode){
            el.style.color = "#" + Math.random().toString().slice(2, 8);
           }
      }
  }
}
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 0 auto;
}

.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
</style>