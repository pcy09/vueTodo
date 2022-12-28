<template>
	<div class="inputBox shadow">
		<input
			type="text"
			placeholder="Type what you have to do"
			v-model="newTodoItem"
			v-on:keyup.enter="addTodo"
		/>
		<span class="addContainer" v-on:click="addTodo"
			><i class="fa-solid fa-square-plus"></i
		></span>
		<AlertModal v-if="showModal">
			<h3 slot="header">경고</h3>
			<span slot="footer" class="modalFooter"
				>할 일을 입력해주세요
				<i
					class="fa-solid fa-circle-xmark closeModalBtn"
					@click="showModal = false"
				></i>
			</span>
		</AlertModal>
	</div>
</template>

<script>
import AlertModal from "./common/AlertModal.vue";
export default {
	components: {
		AlertModal,
	},
	data() {
		return {
			newTodoItem: "",
			showModal: false,
		};
	},

	methods: {
		addTodo() {
			// console.log("새로 입력한 값은?", this.newTodoItem);
			// localStorage.setItem(this.newTodoItem, this.newTodoItem);
			// setItem(키,값) - 로컬스토리지에 데이타를 추가하는 API

			//앞뒤 공백도 입력되는 상황을 막아주기 위해
			if (this.newTodoItem !== "") {
				let value = this.newTodoItem && this.newTodoItem.trim();
				// localStorage.setItem(value, value);  직접 안하고 부모에서 처리
				this.$emit("addTodo", value); //상위 App.vue에 addTodo와 value 전달
				this.clearInput(); //분리, 단일 책임원칙
			} else {
				this.showModal = true;
				// this.showModal = !this.showModal; //토글형식
			}
		},
		clearInput() {
			// 인풋박스 입력 후 초기화
			this.newTodoItem = "";
		},
	},
};
</script>

<style scoped>
.inputBox {
	background-color: #fff;
	height: 50px;
	line-height: 50px;
	border-radius: 5px;
}
input {
	font-size: 16px;
	width: calc(90% - 50px);
	border: none;
}
input:focus {
	outline: none;
}
input:focus::placeholder {
	font-size: 0;
}
span.addContainer {
	float: right;
	width: 50px;
	font-size: 50px;
	background: linear-gradient(to right, #6677ff, #885bc7);
	-webkit-background-clip: text;
	-webkit-text-fill-color: transparent;
}
.closeModalBtn {
	font-size: 30px;
	color: red;
}
.modal-header h3 {
	margin-top: 0;
	color: #42b983;
}
.modalFooter {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	i {
	}
}
</style>
