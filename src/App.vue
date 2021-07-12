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
			listTodo: [
				{ id: 1, title: "học vuejs", completed: true },
				{ id: 2, title: "học angular", completed: false },
			],
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
		},

		handleAddTodo(todo) {
			this.listTodo.push(todo);
		},

		handleUpdateTodo(newTodo) {
			this.listTodo = this.listTodo.map((todo) =>
				todo.id === newTodo.id ? { ...todo, ...newTodo } : todo
			);
		},
	},
};
</script>

<style></style>
