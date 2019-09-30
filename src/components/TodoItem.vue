<template>
	<li>
		<input :checked="todo.completed" type="checkbox" @change='todo.completed = !todo.completed'>
		<span :class='{done: todo.completed }'>
			<strong>{{index + 1}}</strong>
			{{todo.title | upperCase}}
		</span>
		<button @click="$emit('remove-todo', todo.id)">
			&times;
		</button>
	</li>
</template>

<script>
export default {
	props: {
		todo: {
			type: Object,
			required: true
		},
		index: Number
	},
	filters: {
		upperCase(value) {
			return value.toUpperCase();
		}
	}
}
</script>

<style scoped>
span {
	text-align: left;
}

li {
	border: 1px solid #2c3e50;
	border-radius: 5px;
	display: flex;
	justify-content: flex-start;
	align-items: center;
	padding: 5px 20px;
	margin-bottom: 15px;
}

input {
	margin-right: 20px;
}

button {
	font-family: inherit; 
	border-radius: 50%;
	height: 21px;
	margin-left: auto;
}

.done {
	text-decoration: line-through;
}
</style>