<template>
        <section id="section-14" class="slide current" style="">
          <div class="wrap fadeInUp" style="padding-top:100px" >
              
            <div style="margin:0;text-align:center">
                            <!-- <router-link to="/editPost" class="view-btn btn border-primary" style="font-size:2rem">Edit</router-link> -->
                            <button type="button" class="view-btn btn border-primary" data-bs-toggle="modal" data-bs-target="#exampleModal" style="font-size:2rem;">
                      Edit
            </button>
            <button class="view-btn btn border-primary" style="font-size:2rem;margin-left:10px" v-on:click="deletePosts(blog._id)">Delete</button>
            <router-link to="/posts" class="view-btn btn border-primary" style="font-size:2rem;margin-left:10px">Go back</router-link>

            </div>
            <div class="grid vertical-align" v-if="blog" style="margin:0">
              <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
      </div>
      <div class="modal-body" style="margin-top:50px">
        <form>
          <div class="mb-3">
            <label for="recipient-name" class="col-form-label" style="font-size:30px">title</label>
            <input type="text" class="form-control" id="recipient-name" v-model="title" style="font-size:20px">
          </div>
          <div class="mb-3">
            <label for="message-text" class="col-form-label" style="font-size:30px">Description</label>
            <input type="text" class="form-control" id="recipient-name" v-model="body" style="font-size:20px">

          </div>
          <div class="mb-3">
            <label for="message-text" class="col-form-label" style="font-size:30px">Image</label>
            <input type="text" class="form-control" id="recipient-name" v-model="img" style="font-size:20px">

          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-primary" v-on:click="editBlog(blog._id)">Edit</button>
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
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
                <p class="text-intro"><span><img :src="blog.avatar" alt="" class="" style="border-radius:100%;width:2%"></span> {{blog.author}}</p>
                <p class="text-intro">{{blog.date}}</p>
              </div>
              <!-- end .column-->
              <!-- end figure-->
            </div>
            <!-- end .grid-->
          </div>
          <!-- end .wrap-->
      <!-- <div v-else></div> -->
        </section>
</template>

<script>
export default {
props:['id'],
data(){
  return{
    blog:null,
    search:"",
    title:"",
    body:"",
    img:""
  }
},
// mounted() {
//       fetch("http://localhost:5000/posts/", {
//         method: "GET",
//         headers: {
//           "Content-type": "application/json; charset=UTF-8",
//         },
//       })
//         .then((response) => response.json())
//         .then((json) => {
//           this.blogs = json;
//           this.blogs.forEach(async (blog) => {
//             await fetch(
//               "http://localhost:5000/users/" + blog.author,
//               {
//                 method: "GET",
//                 headers: {
//                   "Content-type": "application/json; charset=UTF-8",
//                 },
//               }
//             )
//               .then((response) => response.json())
//               .then((json) => {
//                 blog.author_name = json.name;
//               });
//           });
//         })
//         .catch((err) => {
//           res.send(err)
//         });
//   },
mounted() {
      if(this.id, localStorage.getItem("jwt")){
  fetch("https://socialmediaapp1234.herokuapp.com/posts/" + this.id, {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
        Authorization: `Bearer ${localStorage.getItem("jwt")}`,
      },
    })
      .then((response) => response.json())
      .then( (json) => {
        this.blog = json;
      });
      }
  
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
        })

        .catch((err) => {
          alert(err);
        });
  },
  
    deletePosts: function (id) {
      if (localStorage.getItem("jwt")){
        fetch('https://socialmediaapp1234.herokuapp.com/posts/'+ id ,{
          method: 'DELETE',
          headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
        })
        
        .then(res => res.json())
        .catch(error => console.error('Error:', error))
   
        .then(response => console.log('Success:', response));
        alert("Post Deleted")
         this.$router.push({name:'Posts'});
        
          }
    },
      comments: function(id){
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "Login" });
      }
      fetch("https://socialmediaapp1234.herokuapp.com/posts/" + id, {
        method: "PUT",
        body: JSON.stringify({
          comment:this.comments
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          alert("comment uploaded");
        })
        
        .catch((err) => {
          alert(err);
        });
  },
  
}
  
}
</script>

<style scoped>
.view-btn:hover{
background-color: rgb(55, 55, 241);
color: white;
}

</style>