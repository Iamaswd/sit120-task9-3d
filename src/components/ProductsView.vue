<template>
  <div>
    <!-- product detail rows -->
    <section class="products">
      <h2>Products</h2>
      <p class="section-note">
        Everything here is made from the same two week ferment, which is why the
        four work well together.
      </p>

      <article v-for="product in products" :key="product.name" class="product-row">
        <img :src="product.image" :alt="'Sco-Bio Kombucha ' + product.name">
        <div class="product-info">
          <h3>{{ product.name }}</h3>
          <p class="meta">{{ product.size }} &middot; Step {{ product.step }}</p>
          <p>{{ product.body }}</p>
          <p><strong>Main ingredients:</strong> {{ product.ingredients }}</p>
          <p class="price">{{ product.price }}</p>
        </div>
      </article>
    </section>

    <!-- compare table, the wrapper is what lets it scroll on a phone -->
    <section class="compare alt">
      <h2>Compare the range</h2>
      <p class="section-note">
        All four side by side. On a phone you can swipe the table sideways.
      </p>

      <div class="table-wrap">
        <table>
          <caption>Sco-Bio product comparison</caption>
          <tr>
            <th>Product</th>
            <th>Step</th>
            <th>Size</th>
            <th>Best for</th>
            <th>Use</th>
            <th>Price</th>
          </tr>
          <tr v-for="product in products" :key="product.name">
            <td>{{ product.name }}</td>
            <td>{{ product.step }}</td>
            <td>{{ product.size }}</td>
            <td>{{ product.bestFor }}</td>
            <td>{{ product.use }}</td>
            <td>{{ product.price }}</td>
          </tr>
        </table>
      </div>
    </section>

    <!-- the order to use them in -->
    <section class="routine">
      <h2>How to use them</h2>
      <p class="section-note">
        Morning and night. Each step gets your skin ready for the next one.
      </p>

      <ol class="routine-list">
        <li><strong>Cleanse</strong> with the gel cleanser and rinse with warm water.</li>
        <li><strong>Tone</strong> while your face is still damp.</li>
        <li><strong>Treat</strong> with three or four drops of serum.</li>
        <li><strong>Moisturise</strong> last to seal it all in.</li>
      </ol>
    </section>
  </div>
</template>

<script setup>
import cleanserImg from '../assets/images/cleanser.jpg'
import tonerImg from '../assets/images/toner.jpg'
import serumImg from '../assets/images/serum.jpg'
import moisturizerImg from '../assets/images/moisturizer.jpg'

// one array feeds both the detail rows and the comparison table, so the
// two can never disagree about a price or a size
const products = [
  {
    name: 'Gel Cleanser',
    step: 1,
    size: '105 g',
    price: '$90.00',
    bestFor: 'All skin types',
    use: 'Morning and night',
    ingredients: 'Kombucha ferment, oolong tea extract, glycerin.',
    body: 'A clear gel that foams a little. It takes off sunscreen and the day without that squeaky tight feeling, so you can use it morning and night.',
    image: cleanserImg
  },
  {
    name: 'Toner',
    step: 2,
    size: '100 mL',
    price: '$85.00',
    bestFor: 'All skin types',
    use: 'Morning and night',
    ingredients: 'Kombucha ferment, panthenol, green tea.',
    body: 'Goes on straight after cleansing while your face is still damp. It puts your skin back to its normal pH, which is what lets the serum actually absorb instead of sitting on top.',
    image: tonerImg
  },
  {
    name: 'Serum',
    step: 3,
    size: '30.65 mL',
    price: '$120.00',
    bestFor: 'Dry or dull skin',
    use: 'Night',
    ingredients: 'Kombucha ferment, niacinamide, hyaluronic acid.',
    body: 'Three or four drops is enough for your whole face. This is the one people notice, it evens out dull patches after a few weeks of steady use.',
    image: serumImg
  },
  {
    name: 'Moisturizer',
    step: 4,
    size: '30 g',
    price: '$95.00',
    bestFor: 'Normal to oily skin',
    use: 'Morning and night',
    ingredients: 'Kombucha ferment, squalane, shea butter.',
    body: 'The last step, it locks everything else in. We kept it light on purpose because most of our customers are in humid weather and a heavy cream just sits there.',
    image: moisturizerImg
  }
]
</script>

<style scoped>
.product-row {
  margin-bottom: 1.25rem;
}
</style>
