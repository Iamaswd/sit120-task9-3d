<template>
  <!-- footer -->
  <footer class="site-footer">
    <div class="footer-inner">
      <div>
        <p>Sco-Bio, Deakin Geelong</p>
        <p class="small">&copy; 2026 Sco-Bio. SIT120 Task 9.3D.</p>
      </div>

      <div>
        <p>75 Pigdons Road</p>
        <p>Waurn Ponds, Geelong VIC 3216</p>
        <p><a href="mailto:hello@sco-bio.example">hello@sco-bio.example</a></p>
      </div>

      <!-- secondary nav, the same three pages as the header -->
      <div class="footer-nav">
        <button @click="$emit('navigate', 'home')">Home</button>
        <button @click="$emit('navigate', 'products')">Products</button>
        <button @click="$emit('navigate', 'contact')">Contact</button>
      </div>
    </div>
  </footer>
</template>

<script setup>
defineEmits(['navigate'])
</script>

<style scoped>
.site-footer {
  margin-top: auto;
}
</style>
