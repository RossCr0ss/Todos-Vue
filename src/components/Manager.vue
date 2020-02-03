<template>
  <div class="main">
    <h1>MANAGER</h1>
    <button class="todo-btn-add logOut" v-on:click="logOut($event)">Log Out</button>
    <div class="todo-list">
      <h2>Todo List</h2>
      <div class="flex-between w-40">
        <input
          type="text"
          class="todo-input"
          placeholder="What are you needs to be done?"
          v-model="newTodo"
          @keyup.enter="addTodo"
        />
        <button class="todo-btn-add" @click="addTodo">Add Todo</button>
      </div>

      <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
        {{ todo.title }}
        <div class="flex-between">
          <button class="todo-item-btn todo-item-btn-delete" @click="removeItem(index)">&times;</button>
          <button class="todo-item-btn todo-item-btn-complete" @click="completeTask(index)">&#10004;</button>
        </div>
      </div>

      <div class="flex-between todosCompleted">
        <h2>Completed tasks</h2>
        <div v-for="(todo, index) in todosCompleted" :key="todo.id" class="todo-item-completed">
          {{ todo.title }}
          <div class="flex-between">
            <button
              class="todo-item-btn todo-item-btn-delete"
              @click="removeCompleteItem(index)"
            >&times;</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>



<script>
export default {
  name: "Manager",
  data() {
    return {
      newTodo: "",
      todos: [],
      todosCompleted: []
    };
  },
  computed: {
    isEmptyNewTodo() {
      return this.newTodo !== "";
    }
  },
  methods: {
    addTodo() {
      if (this.isEmptyNewTodo) {
        this.todos.push({
          title: this.newTodo,
          completed: false
        });
        this.newTodo = "";
      } else {
        alert("Your todo field is empty");
      }
    },

    removeItem(index) {
      this.todos.splice(index, 1);
    },

    completeTask(index) {
      this.todosCompleted.push({
        title: this.todos[index].title,
        completed: false
      });
      this.todos.splice(index, 1);
    },

    removeCompleteItem(index) {
      this.todosCompleted.splice(index, 1);
    },
    logOut() {
      this.$router.push("/");
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