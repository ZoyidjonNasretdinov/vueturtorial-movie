<template>
  <input 
    type="text" 
    class="form-control search-input" 
    placeholder="Kinolarni qidirish" 
    :value="term" 
    @input="changeHandler" 
    spellcheck="false"
  />
</template>

<script>
export default {
  data() {
    return {
      term: '',
    };
  },
  methods: {
    changeHandler(e) {
      this.term = e.target.value;
      this.$emit("updateTerm", this.term); // Emit event to parent
    },
  },
};
</script>

<style scoped>
.search-input {
  margin-top: 2rem;
  margin-bottom: 1rem;
  padding: 1.5rem;
  border-radius: 4px;
  background-color: #fcfaf5;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
