<template>
  <div class="todo-list">
    <h1>Aplikasi Pengolahan Data</h1>
      <form @submit.prevent="addTodo">
        <input type="text" v-model="newTodo" placeholder="Input Data..."/>
        <button type="submit" class="tambahkan">Tambahkan</button>
      </form>
      <h2>data indonesia</h2>
      <div class="tengah">
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <input type="checkbox" v-model="todo.done"/>
          <span :class="{ 'done': todo.done }">{{ todo.text }}</span>
          <button @click="removeTodo(index)">Remove</button>
        </li>
      </ul>
      <button @click="removeTodo">Remove All</button>
    </div>
  </div>
  <footer>
    <p>Copyright &copy;ZulfiAkbar</p>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: []
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length === 0) {
        return
      }
      this.todos.push({
        text: this.newTodo,
        done: false
      })
      this.newTodo = ''
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    },
    showAll() {
      this.filter = 'all'
    },
    showActive() {
      this.filter = 'active'
    },
    showCompleted() {
      this.filter = 'completed'
    }
  },
  computed: {
    filteredTodos() {
      switch (this.filter) {
        case 'active':
          return this.todos.filter(todo => !todo.done)
        case 'completed':
          return this.todos.filter(todo => todo.done)
        default:
          return this.todos
      }
    }
  }
}
</script>

<style>

.todo-list {
  max-width: 600px;
  margin: 0 auto;
  padding: 40px;
  font-size: 1.2rem;
  background-color: transparent;
}

.todo-list h1 {
  text-align: center;
  color: black;
}

.todo-list form {
    display: flex;
    margin-bottom: 20px
}

.todo-list input[type=text] {
    flex: 1;
    padding: 8px;
    font-size: 1.2rem;
    border-radius: 10px;
}

.todo-list button[type=submit] {
    margin-left: 10px;
    padding: 8px;
    font-size: 1.2rem;
    background-color: #111;
    border-radius: 10px;
}

.todo-list h2{
  text-align: center;
}

.todo-list ul {
    list-style: none;
    padding: 0;
}

.todo-list li {
    display: flex;
    align-items:center;
    margin-bottom: 10px;
}

.todo-list input[type=checkbox] {
    margin-right: 10px;
}

.todo-list .done {
    text-decoration: line-through;
    color: red;
}

.todo-list button {
    margin-left: 10px;
    padding: 8px;
    background-color: #111;
    border: none;
    cursor: pointer;
    font-size: 1.2rem;
    color: #fff;
    border-radius: 10px;
}

.tengah{
  margin-left: 38%;

}

footer{
  text-align: center;
}

</style>