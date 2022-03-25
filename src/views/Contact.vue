<template>
<section class="bg-primary slide current" id="section-63" style="">
          <span class="background dark" style="background-image:url('https://source.unsplash.com/RkBTPqPEGDo/')"></span>
          <!--.wrap = container (width: 90%) -->
          <div class="wrap size-30">
            <form @submit.prevent="createBlog" class="fadeInUp">
              <fieldset>
                <legend>Contact</legend>
                <p><label>Name</label>
                  <input type="text" tabindex="1" name="title" placeholder="eg james" required="" v-model="title">
                </p>
                <p><label>Email</label>
                  <input type="email" tabindex="1" name="Image" placeholder="example@gmail.com" required="" v-model="email">
                </p>
                <p><label>Message</label>
                  <input type="text" tabindex="1" name="description" placeholder="insert description" required="" v-model="message">
                </p>
                <p>
                  <button type="submit" tabindex="3" title="Login">Submit›</button>
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
}
</script>
<style scoped>
section{
  height: 100vh;
}
form{
  margin-top:150px;
}

</style>
