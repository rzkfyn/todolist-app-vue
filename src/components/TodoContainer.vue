<script>
import UnfinishedTodo from './UnfinishedTodo.vue';
import FinishedTodo from './FinishedTodo.vue';

export default {
  components: { UnfinishedTodo, FinishedTodo },
  emits: [ 'deletebuttonclick', 'unfinishbuttonclick','finishbuttonclick' ],
  props: {
    todos: {
      type: Array,
      default: ''
    }, 
    isFinishedTodosEmpty: {
      type: Boolean,
      default: true
    },
    isUnFinishedTodosEmpty: {
      type: Boolean,
      default: true
    }
  },
  methods: {
    deleteBtnClick(id) {
      this.$emit('deletebuttonclick', id);
    },
    unfinishBtnClick(id) {
      this.$emit('unfinishbuttonclick', id);
    },
    finishBtnClick(id) {
      this.$emit('finishbuttonclick', id);
    }
  }
}
</script>

<template>
  <div class="mt-10 mb-10 py-5 border border-slate-300 px-4 rounded-sm shadow-sm w-full max-w-[500px] mx-auto">
    <h5 class="text-lg text-center text-neutral-700 font-semibold"> To-do list </h5>
    <span class="block mb-5 w-16 mx-auto bg-neutral-400 h-[2px] rounded-md -mt-1"></span>
    <div class="mt-3">
      <h6 class="text-md mt-3 mb-2 font-semibold text-neutral-500">Unfinished Todos</h6>
      <div v-for="todo in todos" class="unfinished-todo">
        <UnfinishedTodo 
        v-if="!todo.finished" 
        :todo="todo"
        @deletebtnclick="deleteBtnClick" 
        @finishbtnclick="finishBtnClick"
        />
      </div>
      <div v-if="isUnFinishedTodosEmpty" class="font-semibold text-md text-red-700 text-sm p-3 bg-red-200/30 border-2 border-red-600 rounded-md">
        Data masih kosong!
      </div>
    </div>

    <div class="mt-10">
      <h6 class="text-md mt-3 mb-2 font-semibold text-neutral-500">Finished Todos</h6>
      <div v-for="todo in todos" class="finished-todo">
        <FinishedTodo 
        v-if="todo.finished" 
        :todo="todo" 
        @deletebtnclick="deleteBtnClick" 
        @unfinishbtnclick="unfinishBtnClick"
        />
      </div>
      <div v-if="isFinishedTodosEmpty" class="font-semibold text-md text-red-700 text-sm p-3 bg-red-200/30 border-2 border-red-600 rounded-md">
        Data masih kosong!
      </div>
    </div>
  </div>
</template>