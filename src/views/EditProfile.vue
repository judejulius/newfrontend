<template>
<section class="bg-primary slide current" id="section-63" style="">
          <span class="background dark" style="background-image:url('https://source.unsplash.com/RkBTPqPEGDo/')"></span>
          <!-- .wrap = container (width: 90%) -->
          <div class="wrap size-30">
            <form @submit.prevent="editProfile" class="fadeInUp">
              <fieldset>
                <legend>Edit Profile</legend>
                <p><label>Name</label>
                  <input type="text" tabindex="1" name="name" placeholder="your@email.com" required="" v-model="name">
                </p>
                <p><label>Contact</label>
                  <input type="text" tabindex="1" name="contact" placeholder="your@email.com" required="" v-model="contact">
                </p>
                <p><label>Email</label>
                  <input type="email" tabindex="1" name="email" placeholder="your@email.com" required="" v-model="email">
                </p>
                <p><label>Password</label>
                  <input type="password" tabindex="2" name="password" placeholder="6 characters minimum" required="" v-model="password">
                </p>
                <p>
                  <button type="submit" tabindex="3" title="Login">Edit ›</button>
                </p>
              </fieldset>
            </form>
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
    editProfile() {
         fetch('https://socialmediaapp1234.herokuapp.com/users/'+ id, {
  method: 'PUT',
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
  .then((json) => console.log(json));
      this.msg = `${ this.name }  Registered Successfuly`;
       alert("Logging in...");
          this.$router.push({ name: "Home" });
    },
  },
};
</script>
<style scoped>
section{
  height: 100vh;
}
form{
  margin-top: 100px;
}
</style>
