<template>
  <div>
    <ul>
      <li v-for="todoItem in todoItems" v-bind:key="todoItem">{{todoItem}}</li>
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
  created: function() {
    // 인스턴스가 생성되자 말자 호출되는 라이프싸이클 훅임.
    // 훅이란 생성되는 시점에 이 안에 로직이 실행되는 것임.
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          console.log(localStorage.key(i));
          this.todoItems.push(localStorage.key(i));
        }
      }
    }
  }
};
</script>

<style>
</style>



