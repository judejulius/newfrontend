<template>
<section class="bg-primary slide current" id="section-63" style="">
          <span class="background dark" style="background-image:url('https://source.unsplash.com/RkBTPqPEGDo/')"></span>
          <!--.wrap = container (width: 90%) -->
          <div class="wrap size-30">
            <form @submit.prevent="login" class="fadeInUp">
              <fieldset>
                <legend>Welcome back</legend>
                <p><label>Email</label>
                  <input type="text" tabindex="1" name="email" placeholder="your@email.com" required="" v-model="email">
                </p>
                <p><label>Password</label>
                  <input type="password" tabindex="2" name="password" placeholder="6 characters minimum" required="" v-model="password">
                </p>
                <p>
                  <button type="submit" tabindex="3" title="Login">Login ›</button>
                </p>
              </fieldset>
            </form>
            <p class="aligncenter">Don't have an account? <router-link to="/signup" title="Sign up">Sign up!</router-link></p>
          </div>
          <!-- .end .wrap -->
        </section>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    login() {
      fetch("https://socialmediaapp1234.herokuapp.com/users", {
        method: "PATCH",
        body: JSON.stringify({
          email: this.email,
          password: this.password,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((response) => response.json())
        .then((json) => {
          localStorage.setItem("jwt", json.jwt);
          localStorage.setItem("id", json.user._id);
          localStorage.setItem("name", json.user.name);
          localStorage.setItem("avatar", json.user.avatar);
          localStorage.setItem("email", json.user.email);
          localStorage.setItem("contact", json.user.contact);
          alert("Welcome back" + " " + json.user.name);
          this.$router.push({ name: "Home" });
        })
        .catch((err) => {
          alert("incorrect creditials");
          this.$router.push({ name: "Login" });
        });
    },
  },
};
</script>
<style scoped>
section{
  height: 100vh;
}
fieldset{
  margin-top: 200px;
  margin-bottom: auto;
}
</style>
