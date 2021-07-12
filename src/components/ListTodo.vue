<template>
	<div class="list-todo w-50 m-auto">
		<AddTodo v-on:handleAdd="handleAdd" />
		<Todo
			v-for="todo in listTodo"
			v-bind:key="todo.id"
			v-bind:todo="todo"
			v-on:changeComplete="changeComplete"
			v-on:removeTodo="removeTodo"
			v-on:updateTodo="updateTodo"
		/>
	</div>
</template>

<script>
import Todo from "./Todo.vue";
import AddTodo from "./AddTodo.vue";

export default {
	name: "ListTodo",
	components: { Todo, AddTodo },
	props: {
		listTodo: Array,
	},

	methods: {
		changeComplete(id) {
			this.$emit("handleCompele", id);
		},

		removeTodo(id) {
			this.$emit("handleRemoveTodo", id);
		},

		handleAdd(todo) {
			this.$emit("handleAddTodo", todo);
		},

		updateTodo(newTodo) {
			this.$emit("handleUpdateTodo", newTodo);
		},
	},
};
</script>

<style></style>
