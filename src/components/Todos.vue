<template>
  <section class="todoapp">
    <!-- header -->
    <header class="header">
      <h1>Todos</h1>
      <input
        type="text"
        class="add-todo"
        placeholder="Create a new todo ..."
        v-model="newTodo"
        @keyup.enter="addTodo"
      />
    </header>
    <!-- end header -->
    <div class="main">
      <!-- list of todos -->
      <ul class="todo-list">
        <li
          class="todo"
          v-for="(todo, i) in todos"
          :key="i"
          :class="{ completed: todo.completed, editing: todo === editing }"
        >
          <input type="checkbox" :id="'todo' + i" v-model="todo.completed" />
          <label :for="'todo' + i" class="title">{{ todo.name }}</label>
          <input
            type="text"
            class="edit"
            v-model="todo.name"
            @keyup.enter="doneEdit"
            v-focus="todo === editing"
          />
          <button @click.prevent="editTodo(todo)">
            <font-awesome-icon
              icon="edit"
              v-model="todo.name"
              style="color: #2f7bf6"
            />
          </button>
          <button @click.prevent="deleteTodo(todo)">
            <font-awesome-icon icon="trash" style="color: #cc444a" />
          </button>
        </li>
      </ul>
      <!-- end list of todos -->
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        {
          name: "Tache n°1",
          completed: false,
        },
        {
          name: "Tache n°2",
          completed: false,
        },
      ],
      newTodo: "",
      editing: null,
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        name: this.newTodo,
        completed: false,
      });
      this.newTodo = "";
      this.saveStorage()
    },
    deleteTodo(todo) {
      //filter among todos the todo you want to delete
      this.todos = this.todos.filter((i) => i !== todo);
      this.saveStorage()
    },
    editTodo(todo) {
      this.editing = todo;
      this.saveStorage()
    },
    doneEdit() {
      this.editing = null;
      this.saveStorage()
    },
    saveStorage() {
      //update the object todos or create it if it doesn't exist
      localStorage.getItem('todos') == null ? localStorage.setItem('todos', JSON.stringify(this.todos)) : localStorage.todos = JSON.stringify(this.todos);
    },
  },
  directives: {
    //focus(): allows you to add a focus on a dom element.
    focus(el, value) {
      if (value) el.focus();
    },
  },
  mounted() {
    //retrieve the todos object if it exists when the page is loaded.
    if (localStorage.todos) {
      this.todos = JSON.parse(localStorage.todos);
    }
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
button {
  background: transparent;
  border: none;
  margin: 10px;
  padding: px;
  -webkit-appearance: none;
  outline: none;
}
button:hover {
  cursor: pointer;
}
:root {
  --fontsize-input: 16px;
  --color-text: #6e757c;
  --color-blue: #2f7bf6;
  --color-red: #cc444a;
}
h1 {
  margin-bottom: 20px;
}
.add-todo,
.todo-list {
  width: 400px;
}
.add-todo {
  height: 20px;
  min-width: 300px;
  border-radius: 3px;
  border: 1px solid #ced4da;
  padding: 5px;
  margin-bottom: 40px;
  font-size: var(--fontsize-input);
  color: var(--color-text);
  outline: none;
}
.todo-list {
  list-style: none;
}
.todo {
  border: 1px solid rgb(236, 236, 236);
}
.todo,
.edit {
  height: 50px;
  margin: 10px 0px;
  padding: 3px 3px 3px 20px;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.edit {
  display: none;
  outline: none;
  font-family: "Poppins", sans-serif !important;
  border: 0;
}
.todo .title,
.edit {
  width: 80%;
  font-size: var(--fontsize-input);
  color: var(--color-text);
}
.title:hover {
  cursor: pointer;
}
.todo button {
  transition: transform 200ms ease-in-out;
}
.todo button:hover {
  transform: scale(1.2);
}
input[type="checkbox"] {
  display: none;
}
.completed .title {
  text-decoration: line-through;
}
.editing {
  padding: 0;
}
.edit {
  padding-top: 0px;
  padding-bottom: 0px;
}
.editing .edit {
  display: flex;
}
.editing label {
  display: none;
}
</style>