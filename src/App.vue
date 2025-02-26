<template>
  <div class="container">
    <h1>Counter {{ counter }}</h1>
    <div class="d-flex">
      <button @click="onDecrement" class="btn btn-danger">-</button>
      <button @click="onIncrement" class="btn btn-success mx-3">+</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      counter : 1 ,
    }
  },

  methods: {
    onIncrement() {
      this.counter += 1
    },

    onDecrement() {
      this.counter -= 1
    }
  },
}
</script>

<style></style>