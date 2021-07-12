<template>
	<div id="app">
		<Header />
		<TodoList
			v-bind:listTodo="listTodo"
			v-on:handleCompele="handleCompele"
			v-on:handleRemoveTodo="handleRemoveTodo"
			v-on:handleAddTodo="handleAddTodo"
			v-on:handleUpdateTodo="handleUpdateTodo"
		/>
	</div>
</template>

<script>
import Header from "./components/Header.vue";
import TodoList from "./components/ListTodo.vue";
export default {
	name: "App",
	components: { Header, TodoList },
	data() {
		return {
			listTodo: JSON.parse(localStorage.getItem("todos"))
				? JSON.parse(localStorage.getItem("todos"))
				: [],
		};
	},

	methods: {
		handleCompele(id) {
			this.listTodo.map((todo) => {
				if (todo.id == id) {
					todo.completed = !todo.completed;
				}
				return todo;
			});
		},

		handleRemoveTodo(id) {
			this.listTodo = this.listTodo.filter((todo) => todo.id !== id);
			localStorage.setItem("todos", JSON.stringify(this.listTodo));
		},

		handleAddTodo(todo) {
			this.listTodo.push(todo);
			localStorage.setItem("todos", JSON.stringify(this.listTodo));
		},

		handleUpdateTodo(newTodo) {
			this.listTodo = this.listTodo.map((todo) =>
				todo.id === newTodo.id ? { ...todo, ...newTodo } : todo
			);

			localStorage.setItem("todos", JSON.stringify(this.listTodo));
		},
	},
};
</script>

<style></style>
