<template>
        <section id="section-14" class="slide current" style="margin-top:100px;">
          <div class="wrap fadeInUp" v-if="blogs">
            <router-link to="/createPost"  class="view-btn btn border-primary" style="font-size:2rem;float:right">Add Post</router-link>
            <h5>Search by author </h5>
            <input type="search" name="" id="search" v-model="search">
            <div class="grid vertical-align" v-for="blog of filterBlogs"
        :key="blog._id"
        :to="{ name: 'Home', params: { id: blog.id } }" style="margin-bottom:100px">
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
                <a href="" class="text-intro"><span><img :src="blog.avatar" alt="" class="" style="border-radius:100%;width:2%"></span> {{blog.author}}</a>
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

    editBlog: function(id){
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "Login" });
      }
      fetch("https://socialmediaapp1234.herokuapp.com/posts/" + id, {
        method: "PUT",
        body: JSON.stringify({
          title: this.title,
          body: this.body,
          img:this.img
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          alert("Post Updated");
        this.$router.go()
        })
        .catch((err) => {
          alert(err);
        });
  }
  },
   computed:{
    filterBlogs:function(){
      return this.blogs.filter((blog) =>{
        return blog.author.match(this.search)
      })
    }
  }
  
}
</script>

<style scoped>
#search{
  width: 20%;
}
.view-btn:hover{
background-color: rgb(55, 55, 241);
color: white;
}
@media only screen and (max-width: 1000px) {
  .wrap {
   margin-top: 50px;
  }
}
@media only screen and (max-width: 800px) {
  .wrap {
   margin-top: 100px;
  }
}
</style>