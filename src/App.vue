<template>
  <div id="app" class="container">
    <img alt="Logo" :src="logoImage" class="logo">
    <router-view></router-view>
    <!-- <login></login> -->
    <!-- <todo-list></todo-list> -->
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import logoImage from './assets/todo-list.png'
import Login from './components/Login'



export default {

  name: 'app',
  components: {
    TodoList,
    Login
  },
  data() {
    return {
      logoImage
    }
  }
}
</script>

<style>

* {
  box-sizing: border-box;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}


#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.logo {
  display: block;
  margin: 10px 0;
  height: 200px;
}


</style>
