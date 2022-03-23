<template>
        <section id="section-14" class="slide current" style="margin-top:100px">
          <div class="wrap fadeInUp" >
              
            
                            <!-- <router-link to="/editPost" class="view-btn btn border-primary" style="font-size:2rem">Edit</router-link> -->
                            <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
                      Edit
            </button>
            <div class="grid vertical-align" v-if="blog" style="margin-top:50px">
              <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                <div class="modal-dialog">
                    <div class="modal-content">
                     <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Edit Your Details Below</h5>
        
                   <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                 </div>
                   <div class="modal-body">
               <form
                  class="requires-validation"
                  @submit.prevent="editPost"
                >
                  <div class="col-md-12">
                    <label >title</label>
                    <input
                      type="text"
                      placeholder="Name"
                      v-model="title"
                    /> <br>
                  </div>

                  <div class="col-md-12">
                      <label for="">desciption</label><br>
                    <input

                      type="text"
                      placeholder="Email"

                      v-model="body"
                    /> <br>
                  </div>
                  <div class="col-md-12">
                      <label for="">image</label><br>
                    <input

                      type="text"
                      v-model="img"
                      placeholder="Password"

                    /> 
                  </div> <br>
                  <div class="form-button mt-3">
                    <button id="submit" type="submit" data-bs-dismiss="modal"  class="btn btn-primary">
                      Edit
                    </button>
                  </div>
                </form> 
      </div>
      <div class="modal-footer">

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
            <router-link to="/posts" class="view-btn btn border-primary" style="font-size:2rem">Go back</router-link>
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
  fetch("https://socialmediaapp1234.herokuapp.com/posts" + this.id, {
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
      editPost(){
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "Login" });
      }
      fetch("https://socialmediaapp1234.herokuapp.com/posts", {
        method: "PUT",
        body: JSON.stringify({
          title:this.title,
          body:this.body,
          img:this.img
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.blog = json
          alert("User Updated");
          this.$router.push({ name: "UserProfile" });
        })
        .catch((err) => {
          alert(err);
        });
  }
}
  
}
</script>

<style scoped>
.view-btn:hover{
background-color: rgb(55, 55, 241);
color: white;
}

</style>