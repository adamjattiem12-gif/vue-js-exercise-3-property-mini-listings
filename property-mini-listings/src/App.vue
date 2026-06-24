<template>
  <div>
    <HeaderSection
      :total-count="properties.length"
      :favourite-count="favouriteCount"
    />

    <main class="container">
      <SearchBar
        v-model="searchQuery"
        :sort-order="sortOrder"
        @update:sort-order="sortOrder = $event"
      />

      <section class="listing-grid" aria-label="Property listings">
        <PropertyCard
          v-for="property in filteredProperties"
          :key="property.id"
          :property="property"
          @toggle-favourite="toggleFavourite"
        />
      </section>

      <p v-if="filteredProperties.length === 0" class="empty">
        No properties match your search.
      </p>
    </main>
  </div>
</template>

<script>
import HeaderSection from './components/HeaderSection.vue'
import PropertyCard from './components/PropertyCard.vue'
import SearchBar from './components/SearchBar.vue'

export default {
  name: 'App',
  components: {
    HeaderSection,
    PropertyCard,
    SearchBar
  },
  data() {
    return {
      searchQuery: '',
      sortOrder: 'low-high',
      properties: [
        {
          id: 1,
          title: 'Sea Point Studio',
          location: 'Sea Point, Cape Town',
          price: 1200,
          type: 'Studio',
          available: true,
          favourite: false,
          image: 'https://images.unsplash.com/photo-1505693416388-ac5ce068fe85?auto=format&fit=crop&w=900&q=80'
        },
        {
          id: 2,
          title: 'City Bowl Loft',
          location: 'Gardens, Cape Town',
          price: 1800,
          type: 'Loft',
          available: false,
          favourite: false,
          image: 'https://images.unsplash.com/photo-1493809842364-78817add7ffb?auto=format&fit=crop&w=900&q=80'
        },
        {
          id: 3,
          title: 'Mountain View Cottage',
          location: 'Vredehoek, Cape Town',
          price: 1500,
          type: 'Cottage',
          available: true,
          favourite: false,
          image: 'https://images.unsplash.com/photo-1512918728675-ed5a9ecdebfd?auto=format&fit=crop&w=900&q=80'
        },
        {
          id: 4,
          title: 'Beach Apartment',
          location: 'Camps Bay, Cape Town',
          price: 3000,
          type: 'Apartment',
          available: true,
          favourite: false,
          image: 'https://images.unsplash.com/photo-1560448204-e02f11c3d0e2?auto=format&fit=crop&w=900&q=80'
        }
      ]
    }
  },
  computed: {
    filteredProperties() {
      const query = this.searchQuery.trim().toLowerCase()
      let results = this.properties.filter((property) => {
        return (
          property.title.toLowerCase().includes(query) ||
          property.location.toLowerCase().includes(query)
        )
      })

      if (this.sortOrder === 'low-high') {
        results.sort((a, b) => a.price - b.price)
      } else {
        results.sort((a, b) => b.price - a.price)
      }

      return results
    },
    favouriteCount() {
      return this.properties.filter((property) => property.favourite).length
    }
  },
  methods: {
    toggleFavourite(propertyId) {
      const property = this.properties.find((item) => item.id === propertyId)

      if (property) {
        property.favourite = !property.favourite
      }
    }
  }
}
</script>
