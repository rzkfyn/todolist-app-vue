<script>
export default {
  emits: [ 'deletebtnclick', 'unfinishbtnclick' ],
  props: {
    todo: {
      type: Object,
      default: {}
    }
  },
  methods: {
    deleteButtonClick(id) {
      this.$emit('deletebtnclick', id);
    },
    unfinishButtonClick(id) {
      this.$emit('unfinishbtnclick', id);
    }
  }
}
</script>

<template>
  <div class="mb-2 px-3 py-2 border border-slate-300 flex justify-between items-center">
    <p class="font-semibold text-neutral-700">
      {{ todo.todo }}
      <p class="text-sm text-neutral-600 font-normal">deadline: {{ todo.deadline }}</p>
    </p>
    <div class="flex">
      <div class="cursor-pointer text-white bg-orange-600 px-3 flex justify-center items-center rounded-md mr-2" title="tandai belum selesai" :data-id="todo.id" @click="unfinishButtonClick($event.target.dataset.id)">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-clockwise" viewBox="0 0 16 16" :data-id="todo.id">
          <path fill-rule="evenodd" d="M8 3a5 5 0 1 0 4.546 2.914.5.5 0 0 1 .908-.417A6 6 0 1 1 8 2v1z" :data-id="todo.id"/>
          <path d="M8 4.466V.534a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384L8.41 4.658A.25.25 0 0 1 8 4.466z" :data-id="todo.id"/>
        </svg>
      </div>

      <div class="cursor-pointer text-white bg-red-600 px-3 flex justify-center items-center rounded-md py-[4px]" title="Hapus todo" :data-id="todo.id" @click="deleteButtonClick($event.target.dataset.id)">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash" viewBox="0 0 16 16" :data-id="todo.id">
          <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z" :data-id="todo.id" />
          <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z" :data-id="todo.id"/>
        </svg>
      </div>
    </div>
  </div>
</template>