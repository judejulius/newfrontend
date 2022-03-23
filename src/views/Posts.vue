<template>
        <section id="section-14" class="slide current" style="margin-top:100px;margin-bottom:100px">
          <div class="wrap fadeInUp" v-if="blogs">
            <router-link to="/createPost"  class="view-btn btn border-primary" style="font-size:2rem;float:right">Add Post</router-link>
            
            <div class="grid vertical-align" v-for="blog of blogs"
        :key="blog._id"
        :to="{ name: 'Home', params: { id: blog.id } }">
         <div class="dropdown text-center" style="float:right">
          <a to="/" class="d-block link-dark text-decoration-none dropdown-toggle" id="dropdownUser1" data-bs-toggle="dropdown" aria-expanded="false">
            </a>
          <ul class="dropdown-menu text-small" aria-labelledby="dropdownUser1">
            <li><button v-on:click="deletePosts(blog.id)">Delete</button></li>
            <li><router-link to="/editPost">Edit</router-link></li>
          </ul>
        </div>
           <div class="column">
                <figure>
                  <img :src="blog.img" class="please" alt="">
                </figure>
              </div>
              <div class="column">
                <h2>
                   {{blog.title}}
                </h2>
                <p class="text-intro">{{blog.body}}</p>
                <router-link to="/profile" class="text-intro"><span><img :src="blog.avatar" alt="" class="" style="border-radius:100%;width:2%"></span> {{blog.author}}</router-link>
                <p class="text-intro">{{blog.date}}</p>
                <router-link :to="{name:'GetOne', params:{id:blog._id}}"  class="view-btn btn border-primary" style="font-size:2rem">View</router-link>
              </div>
              <!-- end .column-->
              <!-- end figure-->
            </div>
            <!-- end .grid-->
          </div>
          <!-- end .wrap-->
      <div v-else></div>
        </section>
</template>

<script>
export default {

data(){
  return{
    blogs:null,
    search:"",
    title:"",
    body:"",
    img:""
  }
},
mounted() {
      fetch("https://socialmediaapp1234.herokuapp.com/posts", {
        method: "GET",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.blogs = json;
          this.blogs.forEach(async (blog) => {
            await fetch(
              "https://socialmediaapp1234.herokuapp.com/users/" + blog.author,
              {
                method: "GET",
                headers: {
                  "Content-type": "application/json; charset=UTF-8",
                },
              }
            )
              .then((response) => response.json())
              .then((json) => {
                blog.author_name = json.name;
              });
          });
        })
        .catch((err) => {
          res.send(err)
        });
  },
  methods:{

    deletePosts: function (id) {
      if (localStorage.getItem("jwt")){
        fetch('http://localhost:5000/posts/'+ id ,{
          method: 'DELETE',
          headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
        })
        
        .then(res => res.json())
        .catch(error => console.error('Error:', error))
   
        .then(response => console.log('Success:', response));
        alert("Note Deleted")
         this.$router.go();
        
          }
    },
            },
   computed:{
    filterBlogs:function(){
      return this.blogs.filter((product) =>{
        return blog .category.match(this.search)
      })
    }
  }
  
}
</script>

<style>
.view-btn:hover{
background-color: rgb(55, 55, 241);
color: white;
}
</style>