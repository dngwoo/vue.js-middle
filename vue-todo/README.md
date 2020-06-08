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
