<template>
  <div id="app" class="container">
    <img alt="Vue logo" :src="logoImage" class="logo">
    <todo-list></todo-list>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import logoImage from './assets/todo-list.png'
import LoginPage from './components/LoginPage'


export default {

  name: 'app',
  components: {
    
    TodoList,
    LoginPage
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
