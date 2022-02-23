<template>
  <section>
    <ul>
      <!-- 여기서의 index는 목록에서 순서, 배열 인덱스와 동일함
          v-for 디렉티브로 반복한 요소는 모두 뷰에서 내부적으로 인덱스를 부여한다. -->
<!--  <li v-for="(todoItem, index) in todoItems" :key="todoItem" class="shadow"> -->
      <li v-for="(todoItem, index) in propsdata" class="shadow">
        <i class="checkBtn fas fa-check" aria-hidden="true"></i>
        {{ todoItem }}
        <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)">
          <i class="far fa-trash-alt" aria-hidden="true"></i>
        </span>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  props: ['propsdata'],
  /* 1. data() : <li> 태그는 propsdata 를 보도록 했으므로 삭제 */
  // data() {
  //   return {
  //     todoItems: []
  //   }
  // },
  /* 2. created() : todoItems 를 관리하는 곳인 App.vue 로 이동 */
  // created() {
  //   if(localStorage.length > 0) {
  //     for(let i =0; i < localStorage.length; i++) {
  //       this.todoItems.push(localStorage.key(i));
  //     }
  //   }
  // },
  methods: {
    /* removeItem() : 로컬 스토리지의 데이터를 삭제
    *   배열.splice(특정인덱스, 숫자) : 특정 인덱스 ~ 부여한 숫자만큼의 인덱스를 삭제함 */
    /* $emit() : '이벤트이름'과 함께 특정 인자도 상위컴포넌트로 전달할 수 있다.
    *   다만 전달받은 인자 값은 상위 컴포넌트에서 참고용으로만 활용하고, 데이터 값은 변경하지 말아야 한다.
    *   컴포넌트는 각자 고유한 유효범위를 갖기 때문에 상위 컴포넌트에서 전달받은 인자값을 갱신하더라도
    *   하위 컴포넌트에는 반영되지 않는다. */
    /* 3. removeTodo() : 'removeTodo' 이벤트를 발생시켜 -> App.vue 의 removeTodo() 메서드를 실행 */
    removeTodo(todoItem, index) {
      console.log(todoItem, index);
      this.$emit('removeTodo', todoItem, index);
      // localStorage.removeItem(todoItem);
      // this.todoItems.splice(index, 1);
    }
  }
}
</script>

<style scoped>
  ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
  }
  li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
  }
  .checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
  }
  .removeBtn {
    margin-left: auto;
    color: #de4343;
  }
</style>
