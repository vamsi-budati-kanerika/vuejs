<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h3>Add User</h3>
      </div>
      <div class="card-body">
        <form v-on:submit.prevent="addUser">
          <div class="form-group">
            <label>Name:</label>
            <input type="text" class="form-control" v-model="user.name" />
          </div>
          <div class="form-group">
            <label>Email:</label>
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
            <input type="submit" class="btn btn-primary" value="Add Item" />
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
  methods: {
    addUser() {
      let uri = "http://localhost:8000/user/create";
      this.axios
        .post(uri, this.user)
        .then((response) => {
          console.log(response.data);
          this.$router.push({ name: "Index" });
        })
        .catch((err) => {
          console.log("error while saving user", err);
        });
    },
  },
};
</script>