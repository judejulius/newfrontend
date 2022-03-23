<template>
<section class="bg-primary slide current" id="section-63" style="">
           <form
    class="container rounded bg-white mb-5 text-center"
    @submit.prevent="editPost"
  v-if="blogs">
    <div class="row">
      <div class="col-md-12 border-right">
        <div class="">
          <div class="d-flex justify-content-between align-items-center mb-3">
            <h4 class="text-right">Edit Product</h4>

          </div>
        </div>
      </div>
      <div class="row mt-2">
        <div class="col-md-12">
          <label class="labels">Title</label
          ><input type="text" class="form-control" v-model="title" />
        </div>
        <div class="col-md-12">
          <label class="labels">Category</label
          ><input type="text" class="form-control" v-model="body" />
          <!-- <select class="form-control" name="category" id="category">
              <option value="masks">Masks</option>
              <option value="wetsuits">Wetsuits</option>
              <option value="camera">Camera</option>
          </select> -->
        </div>
      </div>
      <div class="row mt-3">
        <div class="col-md-12">
          <label class="labels">Img Link</label
          ><input type="text" class="form-control" v-model="img" />
        </div>
      </div>

      <div class="mt-5 text-center">
        <button class="btn btn-primary profile-button" type="submit">
          Confirm Changes
        </button>
      </div>
    </div>
  </form>
        </section>
</template>
<script>
export default {
  props:['id'],
  data() {
    return {
      blogs:null,
      title: "",
      body: "",
      img: "",
    };
  },
 methods: {
    editPost() {
       if (localStorage.getItem("jwt")){
        fetch("https://socialmediaapp1234.herokuapp.com/posts/" + this.id, {
          method: "PUT",
          
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
            alert("Product Updated");
            return this.$router.push({ name: "Posts" });
          });
      }
    },
 },
}
</script>
<style>
section{
  height: 100vh;
}
form{
  margin-top:150px;
}

</style>
