<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
        <i
          class="checkBtn fas fa-check"
          v-bind:class="{checkBtnCompleted: todoItem.completed}"
          v-on:click="toggleComplete(todoItem,index)"
        ></i>
        <span v-bind:class="{textCompleted: todoItem.completed}">{{todoItem.item}}</span>
        <i class="fas fa-trash-alt removeBtn" v-on:click="removeTodo(todoItem, index)"></i>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      todoItems: []
    };
  },
  methods: {
    removeTodo: function(todoItem, index) {
      // console.log(todoItem, index);
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1); // 해당 인덱스에서 한개 요소 제거
    },
    toggleComplete: function(todoItem) {
      todoItem.completed = !todoItem.completed;
      // 로컬 스토리지 데이터 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    }
  },
  created: function() {
    // 인스턴스가 생성되자 말자 호출되는 라이프싸이클 훅임.
    // 훅이란 생성되는 시점에 이 안에 로직이 실행되는 것임.
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          // console.log(localStorage.key(i));
          // this.todoItems.push(localStorage.key(i));

          // console.log(typeof localStorage.getItem(localStorage.key(i))) <- string
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i))) // <- 다시 object로 변경
          );
        }
      }
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
</style>



