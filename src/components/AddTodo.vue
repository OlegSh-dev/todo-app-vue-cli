<template>
	<form @submit.prevent="addTodo">
		<input type="text" v-model="title">
		<button type="submit">Создать задачу</button>
	</form>
</template>

<script>
export default {
	data() {
		return {
			title: ''
		}
	},
	methods: {
		addTodo() {
			if (this.title.trim()) {
				const newTodo = {
					id: Date.now(),
					title: this.title,
					completed: false
				};
				this.$emit('add-todo', newTodo);
				this.title = '';
			}
		}
	}
}
</script>

<style scoped>
form {
	width: 50%;
	margin: 15px auto;
}

input {
	width: 80%;
	margin-right: 5px;
}

button {
	font-family: inherit;
}
</style>