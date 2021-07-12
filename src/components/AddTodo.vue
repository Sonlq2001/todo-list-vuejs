<template>
	<form action="" class="mt-3 mb-3 d-flex" v-on:submit.prevent="addTodo">
		<input
			type="text"
			class="form-control"
			placeholder="Công việc của bạn ?"
			v-model="title"
		/>
		<button class="btn btn-sm btn-primary">Thêm</button>
	</form>
</template>

<script>
export default {
	name: "AddTodo",

	data() {
		return {
			title: "",
		};
	},
	methods: {
		addTodo() {
			if (this.title === "") {
				alert("Bạn chưa nhập công việc nào ?");
			} else {
				const newTodo = {
					id: Math.ceil(Math.random() * 1000),
					title: this.title,
					completed: false,
				};

				this.$emit("handleAdd", newTodo);

				this.title = "";
			}
		},
	},
};
</script>

<style></style>
