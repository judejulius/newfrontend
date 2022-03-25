<template>
<section class="bg-primary slide current" id="section-63" style="">
          <span class="background dark" style="background-image:url('https://source.unsplash.com/RkBTPqPEGDo/')"></span>
          <!--.wrap = container (width: 90%) -->
          <div class="wrap size-30">
            <form @submit.prevent="register" class="fadeInUp">
              <fieldset>
                <legend>Welcome</legend>
                <p><label>Name</label>
                  <input type="text" tabindex="1" name="name" placeholder="eg..Jone" required="" v-model="name">
                </p>
                <p><label>Contact</label>
                  <input type="text" tabindex="1" name="contact" placeholder="0987654321" required="" v-model="contact">
                </p>
                <p><label>Email</label>
                  <input type="email" tabindex="1" name="email" placeholder="your@email.com" required="" v-model="email">
                </p>
                <p><label>Password</label>
                  <input type="password" tabindex="2" name="password" placeholder="6 characters minimum" required="" v-model="password">
                </p>
                <p>
                  <button type="submit" tabindex="3" title="Login">Sign Up ›</button>
                </p>
              </fieldset>
            </form>
            <p class="aligncenter">Already have an account? <router-link to="/login" title="Sign up">Sign in!</router-link></p>
          </div>
          <!-- .end .wrap -->
        </section>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      email: "",
      contact: "",
      password: "",
    };
  },
  methods: {
    register() {
         fetch('https://socialmediaapp1234.herokuapp.com/users/', {
  method: 'POST',
  body: JSON.stringify({
    email:this.email,
    password:this.password,
    name:this.name,
    contact:this.contact,
  }),
  headers: {
    'Content-type': 'application/json; charset=UTF-8',
  },
})
  .then((response) => response.json())
  .then((json) => {
          localStorage.setItem("jwt", json.jwt);

          localStorage.setItem("user", json.user);

  });
      this.msg = `${ this.name }  Registered Successfuly`;
       alert("Registered Successfull");
          this.$router.push({ name: "Login" });
    },
  },
};
</script>
<style scoped>
section{
  height: 100vh;
}
fieldset{
  margin-top: 100px;
  margin-bottom: auto;
}
</style>
