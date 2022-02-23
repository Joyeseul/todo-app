<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fa fa-plus" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal = false">
        할 일을 입력하세요
        <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
      </span>
    </modal>
  </div>
</template>

<script>
import Modal from './common/Modal'

export default {
  /* input 박스에 입력한 텍스트 값을 Vue 에서 인식할 수 있게 됨 */
  data() {
    return {
      newTodoItem: '',
      showModal: false            //모달동작을 위한 flag 값
    }
  },
  /* button 태그와 연결된 메소드를 설정.
  * 로컬 스토리지의 setItem() API 를 사용하여, 입력받은 todoItem 을 추가함.
  * 간단하게 하기 위해 키값과 밸류값 모두 입력받은 텍스트로 저장했다.
  * 값은 개발자도구 - 애플리케이션 탭 - 로컬 스토리지 - http://localhost:8081 에서 확인
  *
  * addTodo()와 clearInput(), 두 개의 메서드로 쪼갠 것은 단일책임원칙(Single Responsibility Principle) 때문임
  *  */
  methods: {
    addTodo() {
      if(this.newTodoItem !== "") {                                     //input 에 값이 있을 때만 저장함
        let value = this.newTodoItem && this.newTodoItem.trim();        //입력값의 앞뒤 공백문자열 제거
        //localStorage.setItem(value, value);
        this.$emit('addTodo', value);                         //직접 Todoinput.vue 에서 처리하는게 아니라 App.vue로 넘김
        this.clearInput();
      } else {
        this.showModal = !this.showModal;                               //텍스트 미입력시 모달 동작
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
  }
}
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
    font-size: 0.9rem;
  }
  .addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: white;
    vertical-align: center;
  }
</style>
