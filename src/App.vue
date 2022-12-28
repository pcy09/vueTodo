<template>
	<div id="app">
		<TodoHeader></TodoHeader>
		<TodoInput v-on:addTodo="addTodo"></TodoInput>
		<TodoList v-bind:propsdata="todoItems" @removeTodo="removeItem"></TodoList>
		<!-- v-bind:프롭스속성이름='전달하고싶은 상위 컴포넌트의 데이타이름' 상위=>하위로 전달 -->
		<TodoFooter @removeAll="clearAll"></TodoFooter>
	</div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
	// name: "App",
	data() {
		return { todoItems: [] }; //로컬 스토리지에 있는 내용을 집어넣을 배열 선언
	},
	// 새로 인식할 때 로컬스토리지에 남아있는 내용으로 배열을 만들어준다.
	created: function () {
		if (localStorage.length > 0) {
			for (let i = 0; i < localStorage.length; i++) {
				this.todoItems.push(localStorage.key(i));
			}
		}
	},
	components: {
		TodoHeader,
		TodoInput,
		TodoList,
		TodoFooter,
	},
	methods: {
		addTodo(value) {
			localStorage.setItem(value, value);
			this.todoItems.push(value);
		},
		clearAll: function () {
			localStorage.clear(); //로컬 스토리지 초기화
			this.todoItems = []; //배열 초기화
		},
		removeItem(item, index) {
			localStorage.removeItem(item); //로컬스토리지에서 삭제
			this.todoItems.splice(index, 1); //splice() - 배열 특정 항목을 제거
		},
	},
};
</script>

<style>
@font-face {
	font-family: "GmarketSansBold";
	src: url("https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2001@1.1/GmarketSansBold.woff")
		format("woff");
	font-weight: normal;
	font-style: normal;
}
@font-face {
	font-family: "Pretendard-Light";
	src: url("https://cdn.jsdelivr.net/gh/Project-Noonnu/noonfonts_2107@1.1/Pretendard-Light.woff")
		format("woff");
	font-weight: 300;
	font-style: normal;
}
body {
	background-color: antiquewhite;
}
#app {
	font-family: "Pretendard-Light", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	max-width: 600px;
	margin: auto;
	margin-top: 30px 3vw;
	position: relative;
}
.shadow {
	box-shadow: 0px 5px 5px rgba(0, 0, 0, 0.2);
}
ul,
li {
	list-style: none;
	margin: 0;
	padding: 0;
}
</style>
