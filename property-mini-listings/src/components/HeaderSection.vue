<template>
  <header class="site-header">
    <h1>Homes &amp; Beyond</h1>
    <p>{{ totalCount }} properties available | {{ favouriteCount }} saved</p>
  </header>
</template>

<script>
export default {
  name: 'HeaderSection',
  props: {
    totalCount: {
      type: Number,
      required: true
    },
    favouriteCount: {
      type: Number,
      required: true
    }
  }
}
</script>
