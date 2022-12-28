<template>
	<div>
		<TransitionGroup name="list" tag="ul">
			<!-- vue 2.2.0 이상에서는 key값 필수 -->
			<li class="shadow" v-for="(item, index) in propsdata" :key="index">
				<i class="checkBtn fa-solid fa-check"></i>
				<span class="text">
					{{ item }}
				</span>
				<span class="removeBtn" @click="removeTodo(item, index)">
					<i class="fa-solid fa-square-minus"></i>
				</span>
			</li>
		</TransitionGroup>
	</div>
</template>

<script>
export default {
	props: ["propsdata"],
	/*  App.vue로 이동
  data() {
    return { todoItems: [] }; //로컬 스토리지에 있는 내용을 집어넣을 배열 선언
  },  
	created: function () {
		if (localStorage.length > 0) {
			for (let i = 0; i < localStorage.length; i++) {
				this.todoItems.push(localStorage.key(i));
			}
		}
	},
  */

	methods: {
		removeTodo: function (item, index) {
			// console.log("밸류 : " + item + ", 키 : " + index);

			this.$emit("removeTodo", item, index);

			// App.vue로 가져감
			// localStorage.removeItem(item); //로컬스토리지에서 삭제
			// this.todoItems.splice(index, 1); //splice() - 배열 특정 항목을 제거
		},
	},
};
</script>

<style scoped>
.list-move, /* 움직이는 엘리먼트에 트랜지션 적용 */
.list-enter-active,
.list-leave-active {
	transition: all 0.5s ease;
}

.list-enter,
.list-leave-to {
	opacity: 0;
	transform: translateX(30px);
}

/* 이동 애니메이션을 올바르게 계산할 수 있도록
   레이아웃 흐름에서 나머지 항목을 꺼내기. */
.list-leave-active {
	position: relative;
}
ul {
	margin: 30px 0;
}
li {
	padding-left: 20px;
	background-color: #fff;
	height: 35px;
	line-height: 35px;
	margin: 10px 0;
	display: flex;
	align-items: center;
	justify-content: space-between;
	border-radius: 5px;
}
.checkBtn {
	font-size: 20px;
	background: linear-gradient(to right, #6677ff, #885bc7);
	-webkit-background-clip: text;
	-webkit-text-fill-color: transparent;
}
.text {
	flex: 1;
	padding: 0 10px;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}
.removeBtn {
	cursor: pointer;
	width: 50px;
	font-size: 25px;
	color: crimson;
}
</style>
