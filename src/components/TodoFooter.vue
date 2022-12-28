<template>
	<div class="clearAllContainer shadow">
		<span @click="clearTodo" class="clearAllBtn">Clear All</span>
	</div>
</template>

<script>
export default {
	methods: {
		clearTodo: function () {
			this.$emit("removeAll");
		},
	},
};
</script>

<style scoped>
.clearAllContainer {
	background-color: #fff;
	border-radius: 5px;
	line-height: 50px;
	width: 100px;
	margin: 0 auto;
	color: crimson;
	cursor: pointer;
}
.clearAllBtn {
	display: block;
}
.clearAllContainer:active {
	background-color: rgb(224, 224, 224);
	transform: translate(0, 2px);
}
</style>
