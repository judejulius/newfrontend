<template>
<section class="bg-primary slide current" id="section-63" style="">
          <span class="background dark" style="background-image:url('https://source.unsplash.com/RkBTPqPEGDo/')"></span>
          <!--.wrap = container (width: 90%) -->
          <div class="wrap size-30">
            <form @submit.prevent="handleSubmit" class="fadeInUp">
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
                name: "",
                email: "",
                subject: "",
                message: "",
            }
        },
        methods: {
            handleSubmit() {
                console.log(`form submitted`)
                console.log(this.name)
                console.log(this.email)
                console.log(this.subject)
                console.log(this.message)
                fetch('https://socialmediaapp1234.herokuapp.com/contact/', {
                        method: "POST",
                        body: JSON.stringify({
                            name: this.name,
                            email: this.email,
                            message: this.message,
                        }),
                        headers: {
                            "Content-type": "application/json; charset=UTF-8"
                        },
                    })
                    .then((response) => response.json())
                    .then((json) => {
                        alert(json.msg)
                        this.name = "",
                            this.email = "",
                            this.contact = "",
                            this.message = ""
                    })
                    .catch((e) => alert(e.msg));
            },
        }
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
