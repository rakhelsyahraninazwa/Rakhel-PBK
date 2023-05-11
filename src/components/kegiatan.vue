<template>
  <div id="app">
    <header>
      <h1>Daftar Kegiatan</h1>
      <div id="todoStatus">
        <div id="totalComp">
          <span id="totalCompleted" class="countData">{{ completedTodoNum }}</span>
          <span class="countName">Selesai</span>
        </div>
        <div id="totalNum">
          <span id="totalTodos" class="countData">{{ todoList.length }}</span>
          <span class="countName">Total</span>
        </div>
      </div>
      <div id="todoFilter">
        <button @click="showAllTodos" :class="{ active: filterType === 'all' }">Semua</button>
        <button @click="showIncompleteTodos" :class="{ active: filterType === 'incomplete' }">Belum Selesai</button>
      </div>
    </header>
    <main>
      <div id="todoInput">
        <div class="listItem-pertama">
          <input type="text" v-model.trim="newTodoName" placeholder="Tambahkan Kegiatan disini..."
            @keydown.enter.prevent="addTodo" @keydown.esc.prevent="removeTodo(todoList[0].id)" />
        </div>
      </div>
      <div id="todoList">
        <div class="listItem" v-for="todo in todosToDisplay" :key="todo.id">
          <input type="checkbox" :checked="todo.done" @change="toggleTodo(todo.id)" />
          <div :class="{ 'todoNameDone': todo.done, 'todoName': !todo.done }"
            @click="toggleTodo(todo.id)">{{ todo.name }}</div>
          <button @click="removeTodo(todo.id)">×</button>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoList: [],
      newTodoName: '',
      filterType: 'all',
    };
  },
  computed: {
    completedTodoNum() {
      return this.todoList.filter(todo => todo.done).length;
    },
    todosToDisplay() {
      if (this.filterType === 'incomplete') {
        return this.todoList.filter(todo => !todo.done);
      } else {
        return this.todoList;
      }
    },
  },
  methods: {
    addTodo() {
      const newTodo = {
        id: this.todoList.length + 1,
        name: this.newTodoName,
        done: false,
      };
      this.todoList.push(newTodo);
      this.newTodoName = '';
    },
    removeTodo(id) {
      this.todoList = this.todoList.filter(todo => todo.id !== id);
    },
    toggleTodo(id) {
      const todo = this.todoList.find(todo => todo.id === id);
      todo.done = !todo.done;
    },
    showAllTodos() {
      this.filterType = 'all';
    },
    showIncompleteTodos() {
      this.filterType = 'incomplete';
    },
  },
};
</script>

<style>

#app {
  max-width: 600px;
  margin: 0 auto;
  background-color: #ffffff;
  border-radius: 10px;
  padding: 20px;
}

body {
  font-family: Arial, sans-serif;
  background-image: url('https://img.freepik.com/premium-vector/shape-background-certificated_49673-123.jpg?w=2000');
  background-size: cover;
}


  header {
display: flex;
justify-content: space-between;
align-items: center;
padding: 20px;
}

h1 {
font-size: 2em;
margin: 0;
}

#todoStatus {
display: flex;
justify-content: space-between;
align-items: center;
font-size: 1.2em;
}

#totalComp,
#totalNum {
display: flex;
flex-direction: column;
}

.countData {
font-weight: bold;
}

.countName {
font-size: 0.8em;
}

#todoFilter {
margin-top: 20px;
display: flex;
justify-content: center;
}

#todoFilter button {
margin: 0 10px;
font-size: 1.2em;
background-color: #fff;
border: none;
padding: 10px 20px;
border-radius: 5px;
cursor: pointer;
}

#todoFilter button.active {
background-color: #ddd;
}

main {
margin-top: 20px;
}

#todoInput {
display: flex;
justify-content: center;
margin-bottom: 20px;
}

.listItem-pertama {
width: 80%;
display: flex;
align-items: center;
padding: 10px;
border-radius: 5px;
background-color: #fff;
box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}

.listItem-pertama input[type='text'] {
width: 100%;
font-size: 1.2em;
border: none;
margin-right: 10px;
}

#todoList {
width: 80%;
margin: 0 auto;
background-color: #f9e1af3d;
padding: 20px;
border-radius: 5px;
box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}

.listItem {
display: flex;
align-items: center;
margin-bottom: 10px;
}

.listItem input[type='checkbox'] {
margin-right: 10px;
}

.listItem .todoName {
flex-grow: 1;
font-size: 1.2em;
}

.listItem .todoNameDone {
flex-grow: 1;
font-size: 1.2em;
text-decoration: line-through;
color: #aaa;
}

.listItem button {
background-color: #fff;
border: none;
cursor: pointer;
font-size: 1.2em;
color: #aaa;
margin-left: 10px;
}

.listItem button:hover {
color: #ff7b7b;
}
#todoFilter {
  display: flex;
  gap: 8px;
}

#todoFilter button {
  background-color: #F45050;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 8px 12px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.2s ease-in-out;
}

#todoFilter button.active {
  background-color: #0077cc;
  color: #fff;
  border-color: #0077cc;
}

#todoFilter button:hover:not(.active) {
  background-color: #F45050;
}
</style>