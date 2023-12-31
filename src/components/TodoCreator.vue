<script setup> // ------------------------------------SCRIPT------------------------------------------- 
import { reactive, defineEmits } from 'vue';
import TodoButton from "./TodoButton.vue";

  const emit = defineEmits(['create-todo']);

  const todoState = reactive({
    todo: "",
    invalid: null,
    errMsg: "",
  }) ; // vai guardar o que o user der de input na variable todo

  const createTodo = () => {
    todoState.invalid = null;
    if (todoState.todo !== "") {
      emit('create-todo', todoState.todo);
      todoState.todo = "";
      return;
    }
    todoState.invalid = true; //tem outro no começo da function pra resetar o invalido, pra ele desconsiderar
    todoState.errMsg = "ToDo value cannot be empty.";
    
  }

</script>

<template> <!-- -------------------------------------TEMPLATE------------------------------------------- -->
    <div class="input-wrap" :class="{ 'input-err' : todoState.invalid }">
        <input type="text" v-model="todoState.todo" /> <!-- v-model to access the property inside the variable-->
        <TodoButton @click="createTodo()"/>
    </div>
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p> <!-- v-if é vue if que só carrega se for, e v-show é sobre mostrar algo if... antes fica display none-->
</template>

<style lang="scss" scoped> //--------------------------------STYLE---------------------------------------
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

  &.input-err {
    border-color: red;
  }

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }
}

.err-msg {
  margin-top: 6px;
  font-size: 12px;
  text-align: center;
  color: red;
}
</style>