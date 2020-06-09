# vue-todo

## Todo App 구현

- [x] 컴포넌트 생성 및 등록하기
- [x] 파비콘, 아이콘, 폰트, 반응형 태그 설정하기
- [x] TodoHeader.vue
- [x] TodoInput.vue 저장기능 구현 (v-model, localStroage.setItem(key,value))
- [x] TodoInput.vue 코드 분할 및 UI 스타일링
- [x] TodoList.vue 할 일 목록 표시 (v-for, localStorage.key(i))
- [x] TodoList.vue 할 일 목록 삭제 기능 (localStorage.removeItem(key), todoItems.splice(index,1))
- [x] TodoList.vue, TodoInput.vue 할 일 완료 기능 구현 (v-for, v-bind, v-on, JSON.parse(), JSON.stringify())
- [x] TodoFooter.vue 구현(localStorage.clear())

## 리팩토링

1. 데이터 관리를 Container 컴포넌트에서 해줘야 한다. Container 컴포넌트는 동작,데이터 조작하는 컴포넌트이다. TodoInput, TodoList, TodoFooter을 단지 화면을 구성하는 Presenter 컴포넌트라고 한다.

- [x] 이것을 위해 App.vue에 TodoList.vue의 data와 created(라이프싸이클 속성)을 가져온다.
- [x] TodoListe.vue의 todoItems를 propsdata로 변경해준다.

2. 할 일 추가 기능

- [x] TodoInput.vue에서 데이터 관리하는 부분 App.uve로 이동. emit으로 이벤트를 발생시켜서 App.vue에서 함수를 실행시킴. newTodoItem를 v-model을 이용해서 input과 연결 시킨 후 그 데이터를 \$emit을 이용해서 같이 보낸다.

3. 할 일 삭제 가능

- [x] TodoList의 removeTodo함수에서 \$emit을 이용하여 이벤트와 todoItem, index를 인자로 보내고 App.vue의 removeOneItem 함수에서 받아서 실행한다.

4. 할 일 완료 기능

- [x] TodoList의 toggleComplete 함수에서 \$emit을 이용하여 이벤트와 todoItem, index를 인자로 보내고 App.vue의 toggleOneItem 함수에서 받아서 실행한다.
- [x] 안티패턴(비효율적인 패턴)을 조심하자. 상위 컴포넌트에서 하위 컴포넌트로 준 데이터를 바꾸지말라는 뜻이다. 데이터는 Container 컴포넌트에서 바꾸는것이 좋다.

```javascript
    toggleOneItem: function(todoItem, index) {
      // todoItem.completed = !todoItem.completed; <- 이렇게 사용하지 말자
      this.todoItems[index].completed = !this.todoItems[index].completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    }
```

5. 할 일 모두 삭제 기능

- [x] TodoFooter의 clearTodo 함수에서 \$emit을 이용하여 이벤트를 보낸다. App.vue에서 이벤트를 받으면 clearAllItems을 실행시킨다. 목록을 지워줘야 되기 때문에 this.todoItems = []로 초기화 해준다.

## 사용자 경험 개선

- [x] 모달 컴포넌트 등록
- [ ] slot을 이용한 모달 오버라이딩
- [x] 내부 트랜지션 사용

## ES6

- [x] const, let

```javascript
// 재설정 불가
let a = 20;
let a = 10; // uncaught syntaxError <- 잡히지 않는 문법(문법 오류)
//---------------------

// 객체로 접근해서 내부 값을 바꾸는 경우는 가능
const a = {};
a.num = 10;

const b = [];
b.push(10);
```

- [x] 변수 스코프와 호이스팅

```javascript
var sum = 5;
sum = sum + i;
function () {}
var i = 10;
// ---------------------- hoisting
var sum;
function (){}
var i;
sum 5;
sum = sum + i;
i = 10;
```

- [x] Arrow Function
- [x] Enhanced Object Literals
- [x] 속성명 축약 특징(객체의 속성명과 값명이 동일할 때 축약가능)
- [x] 자바스크립트 모듈 시스템(import, export)
