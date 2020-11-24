<template>
  <div>
    <h1>Users</h1>

    <table class="table table-hover">
      <thead>
        <tr>
          <td>ID</td>
          <td>Name</td>
          <td>Email</td>
          <td>Phone</td>
          <td>Address</td>
          <td></td>
          <td></td>
        </tr>
      </thead>

      <tbody>
        <tr v-for="user in users" :key="user._id">
          <td>{{ user._id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.phone }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.address }}</td>
          <td>
            <router-link
              :to="{ name: 'Edit', params: { id: user._id } }"
              class="btn btn-primary"
              >Edit</router-link
            >
          </td>
          <td>
            <button class="btn btn-danger" v-on:click="deleteUser(user._id)">
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: []
    };
  },

  created: function () {
    this.fetchUsers();
  },

  methods: {
    fetchUsers() {
      let uri = "http://localhost:8000/user/fetch/all";
      this.axios
        .get(uri)
        .then((response) => {
          console.log("dsd", response);
          this.users = response.data.data;
          console.log(this.users);
        })
        .catch((err) => {
          console.log("error while getting users", err);
        });
    },
    deleteUser(id) {
      let uri = "http://localhost:8000/user/delete/" + id;
      this.axios
        .get(uri)
        .then((resposne) => {
          console.log("delete user response", resposne.data.data);
          location.reload();
        })
        .catch((err) => {
          console.log("error while deleting user", err);
        });
    },
  },
};
</script>