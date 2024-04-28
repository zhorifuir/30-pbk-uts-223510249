<template>
  <div class="container">
    <h1>Iphone cell</h1>
    <div class="input-container">
      <input type="text" v-model="newTodo" placeholder="Tambahkan Tipe Iphone" @keyup.enter="addTodo">
      <button @click="addTodo">Tambah</button>
    </div>
    <div class="todos">
      <div v-for="(todo, index) in filteredTodos" :key="index" :class="{ 'completed': todo.completed }">
        <input type="checkbox" v-model="todo.completed" class="checkbox">
        <span>{{ todo.text }}</span>
        <button @click="cancelTodo(index)">Batal</button>
      </div>
    </div>
    <div class="filter-container">
      <label><input type="checkbox" v-model="showOnlyIncomplete">Tampilkan yang masih ada</label>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
      showOnlyIncomplete: false
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo.trim(), completed: false });
        this.newTodo = '';
      }
    },
    cancelTodo(index) {
      this.todos.splice(index, 1);
    }
  },
  computed: {
    filteredTodos() {
      if (this.showOnlyIncomplete) {
        return this.todos.filter(todo => !todo.completed);
      } else {
        return this.todos;
      }
    }
  }
};
</script>

<style>
body {
  background-image: url(/src/assets/\ bg.png); 
  position: relative;
  background: cover;
background-size: cover;
background-repeat: no-repeat;
}
.container {
  max-width: 400px;
  margin: 30px auto;
  padding: 30px;
  border-radius: 30px;
  background-color:rgb(128, 157, 219)
}
.todos {
  margin-top: 10px;
}

.todos div {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
}

.completed span {
  text-decoration: line-through;
}

.filter-container {
  margin-top: 10px;
}

.filter-container label {
  font-size: 14px;
}
</style>
