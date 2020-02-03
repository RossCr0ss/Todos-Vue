<template>
  <div class="main">
    <button class="todo-btn-add logOut" v-on:click="logOut($event)">Log Out</button>
    <h2>Hello Admin</h2>
    <h3>Create user</h3>

    <form class="flex-col" @submit.prevent="addUser" id="addUser">
      <div class="form-group">
        <label for="username">Create Username</label>

        <input
          type="text"
          name="username"
          v-model="input.username"
          class="form-control todo-input"
          placeholder="Enter login"
        />
      </div>

      <div class="form-group">
        <label for="text">Create Password</label>

        <input
          type="text"
          name="password"
          v-model="input.password"
          class="form-control todo-input"
          placeholder="Enter password"
        />
      </div>

      <button class="todo-btn-add submit" v-on:click="addUser($event)">AddUser</button>

      
    </form>
  </div>
</template>



<script>
export default {
  name: "Admin",
  data() {
    return {
      input: {
        username: "",
        password: ""
      },
      manager: []
    };
  },
  methods: {
    addUser(event) {
      let username = event.target.elements.username.value;
      let password = event.target.elements.password.value;
      let manager = {username, password};

      localStorage.setItem(username, password);

      event.target.reset();
    },
    logOut() {
      window.history.length > 1 ? this.$router.go(-1) : this.$router.push("/");
    }
  }
};
</script>



<style lang="scss">
.flex-col {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.submit {
  width: 150px;
}

.main {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.logOut {
  background-color: rgb(245, 139, 139);
  width: 150px;
}
</style>