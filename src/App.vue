<template>
  <nav>
    <router-link to="/">Main</router-link>
  </nav>
  <router-view />
  <div class="main-recipes">
    <h1>Recipes</h1>
    <div class="main-recipes-container">
      <div class="left-side-recipes">
        <ul>
          <li :class="{ recipe: true, checked: todos[idx].checked }" v-for="(todo, idx) in todos" :key="todo.id" @click="check(idx)">
            {{ todo.text }}
          </li>
        </ul>
      </div>
      <div :class=" [todo.checked ? checkedClass : 'notChecked'] " v-for="todo in todos" :key="todo.id">
          <span v-if="todo.checked">{{ todo.description }}</span>
      </div>
    </div>
  </div>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" />
    <button>Add Todo</button>
  </form>
</template>
<script>
import { throwStatement } from '@babel/types';

// give each todo a unique id
let id = 0;

export default {
  data() {
    return {
      checkedClass: 'rightsiderecipes',
      notChecked: 'notChecked',
      newTodo: "",
      todos: [
        { id: id++, text: "Рецепт 1", checked: false, description: "Тут будет описание у первого рецепта"},
        { id: id++, text: "Рецепт 2", checked: false, description: "Тут будет описание у второго рецепта"},
        { id: id++, text: "Рецепт 3", checked: false, description: "Тут будет описание у третьего рецепта"},
      ],
    };
  },
  methods: {
      addTodo() {
        this.todos.push({ id: id++, text: this.newTodo });
        this.newTodo = "";
      },
      removeTodo(idx) {
        this.todos = this.todos.filter(x => x.id !== idx);
      },
      check(idx) {
        this.todos[idx].checked = !this.todos[idx].checked;
        for(let i = 0; i < this.todos.length; i++) {
          if(this.todos[i].id!=idx) {this.todos[i].checked = false;}
      }
    },
  }
}
</script>
<style lang="scss">
#app {
  font-family: "Dancing Script", cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
.main-recipes {
  width: 50%;
  height: 100%;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  background-color: #2c3e50;
  border-radius: 15px;
  padding: 15px;
}
.main-recipes h1 {
  font-size: 24px;
  color: white;
  margin: 0 auto;
  font-family: "Dancing Script", cursive;
}
.main-recipes-container {
  display: -ms-flex; display: -webkit-flex;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin-top: 30px;
}
.left-side-recipes {
  display: flex;
  flex-wrap: wrap;
  //justify-content: space-between;
  align-items: left;
  background-color: #77a9db;
  width: 38%;
  align-content: flex-start;
  margin-right: 10px;
  padding: 10px;
  border-radius: 10px;
  height: 300px;
  overflow: auto;
}
.rightsiderecipes {
  display: flex;
  flex-wrap: wrap;
  //justify-content: space-between;
  align-items: left;
  background-color: #5bc9c3;
  align-content: flex-start;
  max-width: 60%;
  width: 56%;
  padding: 10px;
  border-radius: 10px;
  height: 300px;
  overflow: auto;
}
.notChecked{
  display: none;
}
ul {
  list-style-type: none;
  width: 100%;
  padding: 0;
}
.recipe {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  max-width: 100%;
  background-color: #42b983;
  margin-top: 10px;
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
}

.checked {
  background-color: red;
}
</style>
