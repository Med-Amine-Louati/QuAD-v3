<template>
  <ul>
    <form >
      <li >
        <br />
        <div class="card" v-for="(post, key) in posts" :key="key">
          <div class="card-header">
            {{ post.companyId }}
          </div>
          <div class="card-body">
            <h5 class="card-title">{{ post.jobTitle }}</h5>
            <p class="card-text">{{ post.Description }}</p>
            <button
              type="submit"
              @click="
                (e) => {
                  e.preventDefault();
                  applying(post.ID);
                }
              "
              id="bnt"
              class="btn btn-primary"
            >
              Apply
            </button>
          </div>
        </div>
        <br />
      </li>
    </form>
  </ul>
</template>
<script>
const axios = require("axios");
export default {
  props: ["data"],
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    applying(postID) {
      console.log(postID);
      const app = {
        jobOfferId: postID,
        userId:"",
      };
      // check !
      console.log(app);
      alert("great you has aplied");
      // send the post id and the user id to the applications table.
      var appsend=app
      appsend.userId=this.data.id
      axios
        .post("http://127.0.0.1:3008/home/apply", appsend)
        .then((response) => console.log("Application saved", response.data))
        .catch((error) => console.log(error));
    },
  },
  mounted() {
    axios
      .get("http://127.0.0.1:3008/jobs")
      .then((response) => {
        console.log("hey", response.data);
        this.posts = response.data;
      })
      .catch((err) => console.log(err));
  },
};
</script>
<style scoped>
.card {
  width: 50%;
  position: relative;
  left: 25%;
}
#bnt {
  float: right;
}
</style>
