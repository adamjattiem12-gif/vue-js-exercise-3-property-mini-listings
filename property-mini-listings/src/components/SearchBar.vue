<template>
  <section class="search-panel">
    <label>
      Search
      <input
        :value="modelValue"
        type="search"
        placeholder="Search by title or location"
        @input="$emit('update:modelValue', $event.target.value)"
      >
    </label>

    <label>
      Sort
      <select
        :value="sortOrder"
        @change="$emit('update:sortOrder', $event.target.value)"
      >
        <option value="low-high">Low to high</option>
        <option value="high-low">High to low</option>
      </select>
    </label>
  </section>
</template>

<script>
export default {
  name: 'SearchBar',
  props: {
    modelValue: {
      type: String,
      default: ''
    },
    sortOrder: {
      type: String,
      required: true
    }
  },
  emits: ['update:modelValue', 'update:sortOrder']
}
</script>
