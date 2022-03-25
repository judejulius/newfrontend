<template>
  <section id="section-47" class="slide current" style="margin-top:100px">
    <h1 class="text-center mb-5">Profile</h1>
    

<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">New message</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <form >
          <div class="mb-3">
            <label for="Name" class="col-form-label">Name:</label>
            <input type="text" class="form-control" id="name" v-model="name">
          </div>
          <div class="mb-3">
            <label for="Email" class="col-form-label">Email:</label>
            <input type="text" class="form-control" id="email" v-model="email">
            
          </div>
          <div class="mb-3">
            <label for="Contact" class="col-form-label">Contact:</label>
            <input type="text" class="form-control" id="contact" v-model="contact">
            
          </div>
        <button type="submit" class="btn btn-primary" v-on:click="editProfile(_id)">edit</button>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
         <div class="card text-left" style="margin-left:auto;margin-right:auto">
  <!-- <img :src="avatar" alt="Avatar" style="width:50%;margin-left:auto;margin-right:auto"> -->
  <div class="container">
    <h4 class="mb-5"><b>Name: {{name}}</b></h4> 
    <h4 class="mb-5"><b>Email: {{email}}</b></h4>
    <h4 class="mb-5"><b>Contact: {{contact}}</b></h4>
  </div>
<button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal" data-bs-whatever="@getbootstrap">Edit</button><br>
<button type="button" class="btn btn-primary" v-on:click="deleteProfile(id)" >Delete</button>
</div>
          <!-- .end .wrap -->
        </section>
</template>

<script>
export default {
  // props:['id'],
data(){
      return{
        user:null,
        id: localStorage.getItem("id"),
        name: localStorage.getItem("name"),
        email: localStorage.getItem("email"),
        avatar: localStorage.getItem("avatar"),
        contact: localStorage.getItem("contact"),


        user:null
      }
    },
    methods:{
      deleteProfile: function (id) {
      if (localStorage.getItem("jwt")){
        fetch('https://socialmediaapp1234.herokuapp.com/users/'+ this.id ,{
          method: 'DELETE',
          headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
        })
        .then((json) => {
          alert("Going to miss you"), 
        this.$router.push({name:'Login'})}
        )
        .catch(error => console.error('Error:', error))
        .then(response => console.log('Success:', response));
        
          }
    },
    },
    editProfile: function(id){
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "Login" });
      }
      fetch("https://socialmediaapp1234.herokuapp.com/users/" + this.id, {
        method: "PUT",
        body: JSON.stringify({
          name: this.name,
          email: this.email,
          contact:this.contact,
          avatar:this.avatar
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
  }
  
}
</script>

<style scoped>
.card{
 box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 25%;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.container {
  padding: 2px 16px;
}
label,input{
  font-size: 2.5rem;
}
</style>