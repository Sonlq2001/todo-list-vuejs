<template>
	<div class="todo d-flex justify-content-between border p-2">
		<div class="todo-left">
			<input
				type="checkbox"
				class="me-2"
				v-bind:checked="todo.completed"
				v-on:change="handleCompele"
			/>
			<!-- <span>{{ todo.title }}</span> -->
			<input
				type="text"
				v-bind:value="todo.title"
				class="input-value"
				@blur="handleBlur($event, todo.id)"
			/>
			<div
				class="overlay-input"
				@click="updateTodo(todo.id)"
				:class="{ active: checkOverlay }"
			></div>

			<span class="finish-todo" v-bind:class="{ active: todo.completed }"
				><ion-icon name="checkmark-circle-outline"></ion-icon
			></span>
		</div>
		<button
			class="btn btn-sm btn-danger"
			v-on:click="handleRemove(todo.id)"
		>
			Xóa
		</button>
	</div>
</template>

<script>
export default {
	name: "Todo",
	props: {
		todo: Object,
	},

	data() {
		return {
			checkOverlay: false,
		};
	},

	methods: {
		handleCompele() {
			this.$emit("changeComplete", this.todo.id);
		},

		handleRemove(id) {
			this.$emit("removeTodo", id);
		},

		updateTodo() {
			this.checkOverlay = !this.checkOverlay;
		},

		handleBlur(e, id) {
			this.checkOverlay = false;

			this.$emit("updateTodo", { title: e.target.value, id });
		},
	},
};
</script>

<style>
.finish-todo.active {
	display: inline-block;
}

.todo-left {
	position: relative;
}

.input-value {
	border: 1px solid #eee;
}
.overlay-input {
	position: absolute;
	top: 0;
	bottom: 0;
	left: 20px;
	width: 190px;
	height: 30px;
}

.overlay-input.active {
	display: none;
}

.finish-todo {
	font-size: 20px;
	color: green;
	margin-left: 20px;
	display: none;
	position: relative;
	top: 5px;
}
</style>
