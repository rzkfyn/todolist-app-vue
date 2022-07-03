<script>
export default {
  emits: [ 'todovaluechange', 'deadlinevaluechange', 'finishedvaluechange', 'ontodosubmit' ],
  data() {
    return {
      inputtodo: '',
      inputdeadline: '',
      inputfinished: false,
    }
  },
  methods: {
    todosubmit() {
      if (this.inputtodo.trim() === '' || this.inputdeadline === '') return;
      this.$emit('ontodosubmit', this.inputtodo);
      return this.reset();
    },
    reset() {
      this.todo = '';
      this.deadline = '';
      this.finished = false;
    }
  },
  computed: {
    todo: {
      get() {
        return this.inputtodo;
      },
      set(val) {
        this.inputtodo = val;
        this.$emit('todovaluechange', this.inputtodo);
      }
    },
    deadline: {
      get() {
        return this.inputdeadline;
      },
      set(val) {
        this.inputdeadline = val;
        this.$emit('deadlinevaluechange', this.inputdeadline);
      }
    },
    finished: {
      get() {
        return this.inputfinished;
      },
      set(val) {
        this.inputfinished = val;
        this.$emit('finishedvaluechange', this.inputfinished);
      }
    }
  }
}
</script>

<template>
  <div class="py-5 px-4 rounded-sm border border-slate-300 mt-10 shadow-sm w-full max-w-[500px] mx-auto">
    <h4 class="text-lg text-center font-semibold">Tambah Todo Baru</h4>
    <form action="" class="mt-5" @submit="$event.preventDefault()">
      <div class="mb-4">
        <label for="todo" class="mb-1 font-semibold text-slate-700">Masukkan todo</label>
        <input v-model="todo" type="text" name="todo" id="todo" autocomplete="off" placeholder="ex: Belajar Vue"
        class="border
        border-slate-400
        focus:outline-none
        w-full
        rounded-sm
        focus:ring-1
        px-2
        py-[3px]
        text-sm
        text-slate-600
        font-semibold
        placeholder:text-sm
        placeholder:font-normal"
        >
      </div>

      <div class="mb-6">
        <label for="deadline" class="mb-1 font-semibold text-slate-700">Batas Waktu</label>
        <input v-model="deadline" type="date" name="deadline" id="deadline"
        class="border
        border-slate-400
        focus:outline-none
        w-full
        rounded-sm
        focus:ring-1
        px-2
        py-[3px]
        text-slate-600
        text-sm
        font-semibold"
        >
      </div>

      <div class="mb-4 flex items-center">
        <input v-model="finished" type="checkbox" name="finished" id="finished" class="cursor-pointer">
        <label for="finished" class="text-sm ml-1 font-semibold text-slate-600">Tandai telah selesai</label>
      </div>

      <div class="flex justify-end">
        <button type="submit" 
        class="text-sm
        font-semibold
        text-white
        py-1
        px-3
        bg-indigo-500
        rounded-md
        hover:bg-indigo-600
        hover:text-neutral-300
        active:bg-indigo-700
        active:text-neutral-500"
        @click="todosubmit">Submit</button>
      </div>
    </form>
  </div>
</template>