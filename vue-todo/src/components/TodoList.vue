<template>
  <div>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem, index) in propsdata" v-bind:key="index" class="shadow">
        <i
          class="checkBtn fas fa-check"
          v-bind:class="{checkBtnCompleted: todoItem.completed}"
          v-on:click="toggleComplete(todoItem,index)"
        ></i>
        <span v-bind:class="{textCompleted: todoItem.completed}">{{todoItem.item}}</span>
        <i class="fas fa-trash-alt removeBtn" v-on:click="removeTodo(todoItem, index)"></i>
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: ["propsdata"],
  methods: {
    removeTodo(todoItem, index) {
      this.$emit("removeItem", todoItem, index);
    },
    toggleComplete(todoItem, index) {
      this.$emit("toggleItem", todoItem, index);
    }
  }
};
</script>

<style scoped>
ul {
  /* 점 없애는 것 */
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  mon-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  line-height: 45px;
  margin-left: auto;
  color: #dc4343;
  cursor: pointer;
}
.removeBtn:active {
  transform: scale(0.9);
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

.list-enter-active,
.list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>



