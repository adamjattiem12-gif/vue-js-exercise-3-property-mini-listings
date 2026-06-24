<template>
  <article class="property-card" :class="{ unavailable: !property.available }">
    <img :src="property.image" :alt="property.title">

    <div class="property-info">
      <span v-if="!property.available" class="badge">Not Available</span>
      <h2>{{ property.title }}</h2>
      <p>{{ property.location }}</p>
      <p>{{ property.type }}</p>
      <p class="price">R{{ property.price }} per night</p>

      <button type="button" @click="$emit('toggleFavourite', property.id)">
        {{ property.favourite ? 'Saved' : 'Save' }}
      </button>
    </div>
  </article>
</template>

<script>
export default {
  name: 'PropertyCard',
  props: {
    property: {
      type: Object,
      required: true
    }
  },
  emits: ['toggleFavourite']
}
</script>
