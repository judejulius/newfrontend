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
          <a to="/" class="d-block link-dark text-decoration-none dropdown-toggle" id="dropdownUser1" data-bs-toggle="dropdown" aria-expanded="false">
            <img src="https://i.postimg.cc/BbR009Pj/fredrik-solli-wandem-V0e-ECO6-ITq-A-unsplash.jpg" alt="mdo" width="32" height="32" class="rounded-circle">
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
methods:{
  logout(){
    localStorage.clear();
    alert('user is logged out')
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

</style>