<template>
  <div>
    <!-- hero section -->
    <section class="hero">
      <div class="hero-text">
        <h1>Softness in every touch</h1>
        <p>
          We ferment our own Kombucha and turn it into four skincare products.
          Nothing extra, recyclable packaging, and never tested on animals.
        </p>
        <button class="button" @click="$emit('navigate', 'products')">
          See the products
        </button>
      </div>

      <div class="hero-image">
        <img :src="heroImg" alt="All four Sco-Bio products">
      </div>
    </section>

    <!-- about section -->
    <section class="about alt">
      <h2>About us</h2>
      <div class="about-inner">
        <img :src="aboutImg" alt="Sco-Bio products on a laboratory stand">
        <div class="about-text">
          <p>
            Sco-Bio started because we were already brewing Kombucha and kept
            reading about what the ferment does for skin. We brew it ourselves
            and let it sit for two weeks, and that liquid is the base of
            everything we sell.
          </p>
          <p>
            We buy our ingredients straight from the growers, bottle in glass,
            and ship in cardboard. Every batch is small so nothing sits around
            losing strength.
          </p>
        </div>
      </div>
    </section>

    <!-- product cards, one column on a phone and four across on a laptop -->
    <section class="products">
      <h2>Our range</h2>
      <p class="section-note">
        Four products made from the same ferment. Use them in this order.
      </p>
      <div class="card-row">
        <article v-for="product in products" :key="product.name" class="card">
          <img :src="product.image" :alt="'Sco-Bio Kombucha ' + product.name">
          <h3>{{ product.name }}</h3>
          <p>{{ product.blurb }}</p>
          <p class="price">{{ product.price }}</p>
        </article>
      </div>
    </section>

    <!-- why kombucha -->
    <section class="reasons alt">
      <h2>Why Kombucha</h2>
      <p class="section-note">
        Three reasons we build everything around the ferment.
      </p>
      <div class="reason-row">
        <div v-for="reason in reasons" :key="reason.heading" class="reason">
          <h3>{{ reason.heading }}</h3>
          <p>{{ reason.body }}</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import heroImg from '../assets/images/hero.jpg'
import aboutImg from '../assets/images/about.jpg'
import cleanserImg from '../assets/images/cleanser.jpg'
import tonerImg from '../assets/images/toner.jpg'
import serumImg from '../assets/images/serum.jpg'
import moisturizerImg from '../assets/images/moisturizer.jpg'

defineEmits(['navigate'])

// the four products as data, so the cards come from one v-for rather than
// four near identical blocks of markup
const products = [
  {
    name: 'Gel Cleanser',
    blurb: 'Oolong tea and Kombucha lift oil and sunscreen without leaving your skin tight.',
    price: '$20.00',
    image: cleanserImg
  },
  {
    name: 'Toner',
    blurb: 'Balances your skin back to its normal pH so whatever comes next soaks in properly.',
    price: '$25.00',
    image: tonerImg
  },
  {
    name: 'Serum',
    blurb: 'A few drops after toning. Brightening, and the heaviest moisture of the four.',
    price: '$35.00',
    image: serumImg
  },
  {
    name: 'Moisturizer',
    blurb: 'Seals the routine in. Light enough to wear in Melbourne summer without feeling greasy.',
    price: '$30.00',
    image: moisturizerImg
  }
]

const reasons = [
  {
    heading: 'It is already active',
    body: 'Fermenting makes the acids and antioxidants for us, so we do not have to add them in a lab.'
  },
  {
    heading: 'Less processing',
    body: 'The ferment does the work, which means fewer steps and less power used getting from tea to bottle.'
  },
  {
    heading: 'One base, four products',
    body: 'Everything starts from the same batch, so the four products layer without fighting each other.'
  }
]
</script>

<style scoped>
/* the button in the hero is a real button now, so it needs the anchor
   styling that .button was giving it */
.hero .button {
  font-family: inherit;
  font-size: 1rem;
  border: none;
  cursor: pointer;
}
</style>
