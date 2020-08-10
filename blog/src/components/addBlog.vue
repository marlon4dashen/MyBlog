<template>
  <div id="add-blog">
    <h2>Add a New Blog Post..</h2>
    <form v-if="!submitted">
        <label>Blog Title:</label>
        <input type='text' v-model.lazy="blog.title" placeholder="Title goes here." required/>
        <label>Blog Content:</label>
        <textarea v-model.lazy="blog.content" placeholder="Content goes here." ></textarea>
        <div id="checkbox">
            <label>Foods and Drinks</label>
            <input type="checkbox" value="Foods" v-model="blog.tags"/>
            <label>Movies</label>
            <input type="checkbox" value="Movies" v-model="blog.tags"/>
            <label>Entertainments</label>
            <input type="checkbox" value="Entertainments" v-model="blog.tags"/>
            <label>Politics</label>
            <input type="checkbox" value="Politics" v-model="blog.tags"/>
        </div>
        <p>Blog Author: </p>
        <select v-model="blog.author">
            <option v-for="author in authors" :key="author"> {{ author }}</option>
        </select>

        <button v-on:click.prevent="post">Add Blogs</button>
    </form>
    <div v-if="submitted">
        <h3>Thanks for adding your post.</h3>
    </div>
    <div id="preview">
        <h3>Preview Blog</h3>
        <p>Blog title: {{ blog.title }}</p>
        <p>Blog content: </p>
        <p>{{ blog.content }}</p>
        <p>Blog tags: </p>
        <ul>
            <li v-for="(tag, index) in blog.tags" :key="blog.tags[index]">{{ tag }}</li>
        </ul>
        <p>Blog author: {{ blog.author }}</p>

    </div>
  </div>
</template>

<script>
export default {

  data () {
    return {
        blog:{
            title:'',
            content: '',
            tags: [],
            author: ''
        },
        authors:[
            'Alice', 'Marlon', 'Jack', 'Niu', 'cc'
        ],
        submitted: false,
    }
  },

  methods: {
      post: function(){
          this.$http.post('https://arched-glow-257422.firebaseio.com/posts.json',this.blog).then(function(data){
              console.log(data);
              this.submitted = true;
          });
      }
  }

  
}
</script>

<style>
#add-blog *{
    box-sizing: border-box;
    background: linear-gradient(to right)
}

#add-blog{
    margin: 20px auto;
    max-width: 500px;
}
label{
    display: block;
    margin: 20px 0 10px;
}

input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
    border-radius: 5px;
    
}
#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}
h3{
    margin-top: 10px;
}

#checkbox label{
    display: inline-block;
    margin-right: 10px;
}

#checkbox input{
    display: inline-block;
    margin-right: 10px;
}
</style>
