<template>
  <header class="p-3 border-bottom bg-white fixed-top" >
    <div class="container">
      <div class="d-flex flex-wrap align-items-center justify-content-center justify-content-lg-start ">
        <a href="/" class="mb-2 mb-lg-0 text-dark text-decoration-none">
          <img src="../assets/jj.jpg" style="width:10%">
        </a>

        <ul class="nav col-12 col-lg-auto me-lg-auto mb-2 justify-content-center mb-md-0">
          <li><router-link to="/" class="nav-link px-2 link-dark">Home</router-link></li>
          <li><router-link to="/about" class="nav-link px-2 link-dark">About</router-link></li>
          <li><router-link to="/posts" class="nav-link px-2 link-dark">Posts</router-link></li>
          <li><router-link to="/contact" class="nav-link px-2 link-dark">Contact</router-link></li>  
        </ul>

        <div class="dropdown text-end">
          <a to="/" class="d-block link-dark text-decoration-none" id="dropdownUser1" data-bs-toggle="dropdown" aria-expanded="false">
          <i class="bi bi-arrow-down-circle-fill" style="font-size:2.5rem"></i>
           <p>{{name}}</p>
          </a>
          <ul class="dropdown-menu text-small" aria-labelledby="dropdownUser1">
            <!-- <li><router-link class="dropdown-item" to="/createpost" style="font-size:18px">Add post</router-link></li> -->
            <li><router-link class="dropdown-item" to="/profile" style="font-size:18px">Profile</router-link></li>
            <li><router-link class="dropdown-item" to="/login" style="font-size:18px">Login</router-link></li>
            <li><hr class="dropdown-divider"></li>
          
            <li><router-link class="dropdown-item" to="/login" style="font-size:18px" v-on:click="logout">Sign out</router-link></li>
          </ul>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  data(){
    return{
name: localStorage.getItem("name"),
    }
  },
methods:{
  logout(){
    alert('GoodBye' + " " + json.user.name)
    localStorage.clear();
    this.$router.push({name:'Login'})
  }
}
}
</script>

<style>
ul li{
  font-size: 25px;
}
.active:hover,a.router-link-active{
    content: '';
  border-bottom: 2px solid rgb(55, 55, 241);
  padding: 0px ;
  text-decoration: none;
  box-shadow: none;
}
.dropdown:hover{
  cursor: pointer;
}
</style>