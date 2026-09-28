<template>
  <!-- header -->
  <header class="site-header">
    <p class="logo">Sco-Bio</p>
    <p class="tagline">Ecofriendly skincare from Kombucha</p>
  </header>

  <!-- nav bar, the same three pages from the 1.1p wireframes -->
  <nav class="site-nav">
    <button
      v-for="page in pages"
      :key="page.id"
      :class="{ current: page.id === activeView }"
      @click="$emit('navigate', page.id)"
    >
      {{ page.label }}
    </button>
  </nav>
</template>

<script setup>
// which page is showing, so the current one can be underlined
defineProps({
  activeView: {
    type: String,
    default: 'home'
  }
})

// sends the chosen page id up to App.vue, which owns the view state
defineEmits(['navigate'])

const pages = [
  { id: 'home', label: 'Home' },
  { id: 'products', label: 'Products' },
  { id: 'contact', label: 'Contact' }
]
</script>

<style scoped>
.site-nav {
  margin-bottom: 0;
}
</style>
