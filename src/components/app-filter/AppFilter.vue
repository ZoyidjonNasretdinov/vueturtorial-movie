<template>
  <div class="btn-group">
    <button 
      v-for="option in filterOptions" 
      :key="option.value"
      :class="['btn', filter === option.value ? 'btn-dark' : 'btn-outline-dark']" 
      type="button" 
      @click="filterHandler(option.value)"
    >
      {{ option.label }}
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      filter: "all", // Default filter state
      filterOptions: [
        { value: "all", label: "Barcha kinolar" },
        { value: "popular", label: "Mashhur kinolar" },
        { value: "mostViewers", label: "Eng ko'p ko'rilgan kinolar" },
      ],
    };
  },
  methods: {
    filterHandler(filter) {
      this.filter = filter; // Update active filter
      this.$emit("updateFilter", filter); // Emit event to parent
    }
  }
};
</script>

<style scoped>
.btn-group {
  margin-top: 1rem;
}
</style>
