<script>
import TopBar from './components/TopBar.vue';
import TodoForm from './components/TodoForm.vue';
import TodoContainer from './components/TodoContainer.vue';
import Footer from './components/Footer.vue';

export default {
  components: { TopBar, TodoForm, TodoContainer, Footer },
  data() {
    return {
      inputtodo: '',
      inputdeadline: '',
      inputfinished: false,
      todos: [],
      finishedTodosEmpty: true,
      unFinishedTodosEmpty: true
    }
  },
  methods: {
    setTodo(val) {
      this.inputtodo = val;
    },
    setDeadline(val) {
      this.inputdeadline = val;
    },
    setFinished(val) {
      this.inputfinished = val;
    },
    isTodoEmpty() {
      this.finishedTodosEmpty = !this.todos.some(todo => todo.finished === true);
      this.unFinishedTodosEmpty = !this.todos.some(todo => todo.finished !== true);
    },
    saveTodos(todos) {
      localStorage.setItem('todos', todos);
    },
    addTodo() {
      this.todos.unshift({
        todo: this.inputtodo,
        deadline: this.inputdeadline,
        finished: this.inputfinished,
        id: + new Date()
      });
      this.saveTodos(JSON.stringify(this.todos));
      this.isTodoEmpty();
    },
    deleteTodo(id) {
      const index = this.todos.findIndex(todo => todo.id === parseInt(id));
      if (!confirm(`Apakah kamu yakin ingin menghapus ${this.todos[index].todo}?`)) return;
      this.todos.splice(index, 1);
      this.saveTodos(JSON.stringify(this.todos));
      this.isTodoEmpty();
    },
    setAsUnfinished(id) {
      const index = this.todos.findIndex(todo => todo.id === parseInt(id))
      this.todos[index] = {
        ...this.todos[index],
        finished: false
      }
      this.saveTodos(JSON.stringify(this.todos));
      this.isTodoEmpty();
    },
    setAsFinished(id) {
      const index = this.todos.findIndex(todo => todo.id === parseInt(id))
      this.todos[index] = {
        ...this.todos[index],
        finished: true
      }
      this.saveTodos(JSON.stringify(this.todos));
      this.isTodoEmpty();
    }    
  },
  mounted() {
    if (!localStorage.getItem('todos')) return this.saveTodos('[]');
    this.todos = JSON.parse(localStorage.getItem('todos'));
    this.isTodoEmpty();
  }
}
</script>

<template>
  <TopBar/>
  <main class="px-2 w-full max-w-[750px] mx-auto">
    <TodoForm 
    @todovaluechange="setTodo" 
    @deadlinevaluechange="setDeadline" 
    @finishedvaluechange="setFinished" 
    @ontodosubmit="addTodo" 
    />
    <TodoContainer 
    :todos="todos" 
    :isFinishedTodosEmpty="finishedTodosEmpty" 
    :isUnFinishedTodosEmpty="unFinishedTodosEmpty"
    @deletebuttonclick="deleteTodo"
    @unfinishbuttonclick="setAsUnfinished"
    @finishbuttonclick="setAsFinished"
    />
  </main>
  <Footer/>
</template>