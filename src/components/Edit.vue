<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h3>Edit User</h3>
      </div>
      <div class="card-body">
        <form v-on:submit.prevent="updateUser">
          <div class="form-group">
            <label>Name:</label>
            <input type="text" class="form-control" v-model="user.name" />
          </div>
          <div class="form-group">
            <label>User Email:</label>
            <input type="text" class="form-control" v-model="user.email" />
          </div>
          <div class="form-group">
            <label>Phone:</label>
            <input type="text" class="form-control" v-model="user.phone" />
          </div>
          <div class="form-group">
            <label>Address:</label>
            <input type="text" class="form-control" v-model="user.address" />
          </div>
          <div class="form-group">
            <input type="submit" class="btn btn-primary" value="Update User" />
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      user: {},
    };
  },
  created: function () {
    this.getUser();
  },
  methods: {
    getUser() {
      let uri = "http://localhost:8000/user/fetch/" + this.$route.params.id;
      this.axios
        .get(uri)
        .then((response) => {
          this.user = response.data.data;
        })
        .catch((err) => {
          console.log("error while fetching user", err);
        });
    },

    updateUser() {
      let uri = "http://localhost:8000/user/update/" + this.$route.params.id;
      this.axios
        .post(uri, this.user)
        .then(() => {
          this.$router.push({ name: "Index" });
        })
        .catch((err) => {
          console.log("error while updating user", err);
        });
    },
  },
};
</script>