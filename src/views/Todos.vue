<template>
  <div>
	<router-link to="/">Home</router-link>

    <AddTodo
      @add-todo="addTodo"
    />

    <select v-model="filter">
      <option value="all">Все</option>
      <option value="completed">Завершенные</option>
      <option value="not-completed">Активные</option>
    </select>
    
    <Loader v-if="loading" />

    <TodoList
		v-else-if="filteredTodos.length"
      	:todos='filteredTodos'
      	@remove-todo='removeTodo'
    />
	<p v-else>Нет задач</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo';
import Loader from '@/components/Loader';
export default {
  name: 'app',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  components: {
    TodoList, AddTodo, Loader
  },
  computed: { 
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos
      }
      if (this.filter === 'completed') {
        return this.todos.filter((todo) => todo.completed)
      }
      if (this. filter === 'not-completed') {
        return this.todos.filter((todo) => !todo.completed)
      }
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json;
          this.loading = false;
        }, 1000);
      });
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(el => el.id != id);
    }, 
    addTodo(todo) {
      this.todos.push(todo);
    }
  }
};
</script>

<style scoped>
select {
  display: block;
  margin: 15px auto;
}

:link {
	text-decoration: none;
	color: rgb(92, 170, 219);
}

:visited {
	color: rgb(92, 170, 219);
}
</style>