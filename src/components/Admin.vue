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
    <br>

    <form class="flex-col" @submit.prevent="deleteUser" id="deleteUser">
      <div class="form-group">
        <label for="text">Delete User</label>

        <input
          type="text"
          name="user"
          v-model="input.user"
          class="form-control todo-input"
          placeholder="Enter user"
        />
      </div>

      <button class="todo-btn-add submit" v-on:click="deleteUser($event)">deleteUser</button>

  
    </form>

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
  name: "Admin",
  data() {
    return {
      input: {
        username: "",
        password: ""
      },
      manager: [],
      newTodo: "",
      todos: [
        {
          title: "Learn Vue.js",
          completed: false
        },
        {
          title: "Open VS Code",
          completed: false
        },
        {
          title: "Finish todo-vue task",
          completed: false
        }
      ],
      todosCompleted: []
    };

  },
  computed: {
    isEmptyNewTodo() {
      return this.newTodo !== "";
    }
  },
  methods: {
    addUser(event) {
      let username = event.target.elements.username.value;
      let password = event.target.elements.password.value;
      let manager = {username, password};
      /* this.manager.push({ manager }); */

        /* localStorage.manager = JSON.stringify(); */

      let managerJSON = JSON.stringify(username, password);
      console.log(managerJSON)
      localStorage.setItem(username, password);
      event.target.reset();
    },


    deleteUser(event) {
        let user = event.target.elements.user.value;
        console.log(user)
        localStorage.removeItem(user);
    },

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

.w-40 {
  width: 40vw;
}

.todo-list {
  margin-top: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.flex-between {
  display: flex;
  justify-content: space-between;
}

.todosCompleted {
  border-radius: 6px;
  background-color: rgb(161, 226, 161);
  min-height: 200px;
  width: 100%;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
  justify-content: flex-start;
}

.todo-input {
  width: 85%;
  min-width: 300px;
  padding: 10px 18px;
  font-size: 18px;
  margin: 10px 0;
  border-radius: 6px;
  border: 3px solid rgb(101, 182, 101);

  &:focus {
    outline: 0;
  }
}

.todo-btn-add {
  border: 0;
  border-radius: 6px;
  width: 15%;
  background-color: rgb(101, 182, 101);
  font-size: 18px;
  color: #fff;
  margin: 10px 0 0 5px;
  height: 48px;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 6px 18px;
  border: 1px solid rgb(101, 182, 101);
  width: 40vw;
  min-width: 300px;
  margin-bottom: 5px;
  border-radius: 4px;

  &-completed {
    width: 38vw;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 6px 18px;
    border: 3px solid rgb(101, 182, 101);
    min-width: 300px;
    margin-bottom: 5px;
    border-radius: 4px;
    background: #fff;
  }

  &-btn {
    color: #fff;
    border: 0;
    border-radius: 4px;
    width: 20px;
    height: 20px;
    text-align: center;
    font-weight: 700;
    margin-left: 5px;

    &-delete {
      background: rgb(201, 42, 42);
    }

    &-complete {
      background-color: rgb(30, 180, 30);
      font-size: 12px;
    }
  }
}
</style>