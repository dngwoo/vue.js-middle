<template>
  <div class="inputBox shadow">
    <!-- v-model을 사용하여 input과 data값을 동적으로 매핑 -->
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodo" />
    <span class="addContainer" @click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
    <Mdoal v-if="showModal" @close="showModal = false">
      <!--
      you can use custom content here to overwrite
      default content
      -->
      <h3 slot="header">
        경고!
        <i
          class="fas fa-times closeModalBtn fa-2x"
          @click="showModal = false"
        ></i>
      </h3>
      <div slot="body">무엇이라도 입력하세요</div>
    </Mdoal>
  </div>
</template>

<script>
import Modal from "./common/Modal.vue";
export default {
  data() {
    return {
      newTodoItem: "", // input value 값을 받아온다.
      showModal: false,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== "") {
        const text = this.newTodoItem.trim(); // 앞 뒤 공백제거
        // this.$emit("addTodo", this.newTodoItem);
        this.$store.commit("addOneItem", text);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = "";
    },
  },
  compononents: {
    Modal,
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-weight: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478f8, #8763f8);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
  cursor: pointer;
}
.addBtn:active {
  transform: scale(0.9);
}
.closeModalBtn {
  color: #42b983;
  vertical-align: middle;
}
</style>
