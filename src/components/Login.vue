<template>
  <div class="main">
    <h2>Login</h2>

    <form class="flex-col" @submit.prevent="login" id="login">
      <div class="form-group">
        <label for="username">Username</label>

        <input
          type="text"
          name="username"
          v-model="input.username"
          class="form-control todo-input"
          placeholder="Enter your login"
        />
      </div>

      <div class="form-group">
        <label for="password">Password</label>

        <input
          type="password"
          name="password"
          v-model="input.password"
          class="form-control todo-input"
          placeholder="Enter your password"
        />
      </div>

      <button class="todo-btn-add submit" v-on:click="login($event)">Login</button>
    </form>
  </div>
</template>



<script>
export default {
  name: "Login",
  data() {
    return {
      input: {
        username: "",
        password: ""
      },
      admin: {
        username: "admin",
        password: "qwerty"
      }
    };
  },
  methods: {
    login(event) {
      let keys = Object.keys(localStorage);
      for (let key of keys) {
        if (
          key == event.target.elements.username.value &&
          localStorage.getItem(key) == event.target.elements.password.value
        ) {
          return this.$router.push("/manager");
        } else if (
          event.target.elements.username.value == this.admin.username &&
          event.target.elements.password.value == this.admin.password
        ) {
          this.$router.push("/admin");
        } else {
          console.log('Invalid dataf')
        }
      }

      /* if (
        event.target.elements.username.value == this.admin.username &&
        event.target.elements.password.value == this.admin.password
      ) {
        this.$router.push("/admin");
      } else {
        alert("Invalid data!");
      } */
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
</style>