<template>
  <section class="todoapp">
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
    <div class="main">
      <ul class="todo-list">
        <li class="todo" v-for="(todo, i) in todos" :key="i" :class="{completed: todo.completed}">
          <input
            type="checkbox"
            :id="'todo'+i"
            v-model="todo.completed"
          />
            <label :for="'todo'+i" class="title">{{ todo.name }}</label>
          <button>
            <font-awesome-icon icon="edit" style="color: #2f7bf6" />
          </button>
          <button>
            <font-awesome-icon icon="trash" style="color: #cc444a" />
          </button>
        </li>
      </ul>
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
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        name: this.newTodo,
        completed: false,
      });
      this.newTodo = "";
    },
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
  height: 50px;
  margin: 10px 0px;
  padding: 3px 3px 3px 20px;
  display: flex;
  flex-direction: row;
  display: flex;
  align-items: center;
  border: 1px solid rgb(236, 236, 236);
}
.todo .title {
  width: 80%;
  font-size: var(--fontsize-input);
  color: var(--color-text);
}
.todo button {
  transition: transform 200ms ease-in-out;
}
.todo button:hover {
  transform: scale(1.2);
}
input[type="checkbox"]{
    display:none
}
.completed .title{
    text-decoration: line-through;
}
</style>