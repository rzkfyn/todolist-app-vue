<script>
export default {
  methods: {
    toroot() {
      location.href = '/';
    }
  }
}
</script>

<template>
  <div class="p-3 bg-indigo-600 shadow-md sticky top-0 w-full max-w-[750px] mx-auto rounded-sm">
    <h4 class="text-white text-center font-semibold cursor-pointer text-lg" @click="toroot">Simple To-do App</h4>
  </div>
</template>