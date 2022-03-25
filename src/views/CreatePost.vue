<template>
<section class="bg-primary slide current" id="section-63" style="">
          <span class="background dark" style="background-image:url('https://source.unsplash.com/RkBTPqPEGDo/')"></span>
          <!--.wrap = container (width: 90%) -->
          <div class="wrap size-30">
            <form @submit.prevent="createBlog" class="fadeInUp">
              <fieldset>
                <legend>Add Post</legend>
                <p><label>title</label>
                  <input type="text" tabindex="1" name="title" placeholder="insert post title" required="" v-model="title">
                </p>
                <p><label>Post img</label>
                  <input type="text" tabindex="1" name="Image" placeholder="insert url" required="" v-model="img">
                </p>
                <p><label>Description</label>
                  <input type="text" tabindex="1" name="description" placeholder="insert description" required="" v-model="body">
                </p>
                <p>
                  <button type="submit" tabindex="3" title="Login">Add post ›</button>
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
      title: "",
      body: "",
      img: "",
    };
  },
  methods: {
    createBlog() {
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        this.$router.push({ name: "Login" });
      }
      fetch("https://socialmediaapp1234.herokuapp.com/posts", {
        method: "POST",
        body: JSON.stringify({
          title: this.title,
          body: this.body,
          img: this.img,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          alert("Post Created");
          this.$router.push({ name: "Posts" });
        })
        .catch((err) => {
          alert(err);
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
form{
  margin-top:150px;
}

</style>
