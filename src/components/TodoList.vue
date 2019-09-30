<template>
	<div>
		<ul>
			<TodoItem
				:todo="todo"
				v-for="(todo, i) of todos"
				:index="i"
				@remove-todo="removeTodo"
			/>
		</ul>
	</div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
	props: ['todos'],
	components: {
		TodoItem
	},
	methods: {
		removeTodo(id) {
			this.$emit('remove-todo', id);
		}
	}
}
</script>

<style scoped>
ul {
	width: 60%;
	list-style: none;
	margin: 30px auto;
	padding: 0;
}
</style>