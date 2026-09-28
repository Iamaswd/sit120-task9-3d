<template>
  <div>
    <!-- ways to reach us -->
    <section class="contact">
      <h2>Get in touch</h2>
      <p class="section-note">
        We answer emails within two working days. If your order has gone missing,
        send us the order number and we will chase it.
      </p>

      <div class="contact-row">
        <div v-for="card in contactCards" :key="card.heading" class="contact-card">
          <h3>{{ card.heading }}</h3>
          <p v-for="line in card.lines" :key="line">{{ line }}</p>
        </div>
      </div>
    </section>

    <!-- stockists, the wrapper is what lets the table scroll on a phone -->
    <section class="stockists alt">
      <h2>Where to buy</h2>
      <p class="section-note">
        Five shops carry the range. On a phone you can swipe the table sideways
        to see the rest of the columns.
      </p>

      <div class="table-wrap">
        <table>
          <caption>Shops stocking Sco-Bio</caption>
          <tr>
            <th>Shop</th>
            <th>Suburb</th>
            <th>Stocks</th>
            <th>Open</th>
          </tr>
          <tr v-for="shop in stockists" :key="shop.name">
            <td>{{ shop.name }}</td>
            <td>{{ shop.suburb }}</td>
            <td>{{ shop.stocks }}</td>
            <td>{{ shop.open }}</td>
          </tr>
        </table>
      </div>
    </section>

    <!-- questions we get asked a lot -->
    <section class="faq">
      <h2>Questions we get asked</h2>
      <p class="section-note">
        If yours is not here, email us and we will add it.
      </p>

      <div class="faq-row">
        <div v-for="item in faqs" :key="item.question" class="faq-item">
          <h3>{{ item.question }}</h3>
          <p>{{ item.answer }}</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
const contactCards = [
  { heading: 'Email', lines: ['hello@sco-bio.example'] },
  { heading: 'Studio', lines: ['75 Pigdons Road', 'Waurn Ponds, Geelong VIC 3216'] },
  { heading: 'Markets', lines: ['Geelong Makers Market', 'Every second Sunday, 9am to 2pm'] }
]

const stockists = [
  { name: 'Shop 1', suburb: 'Waurn Ponds', stocks: 'Full range', open: 'Mon to Sat' },
  { name: 'Shop 2', suburb: 'Waurn Ponds', stocks: 'Full range', open: 'Tue to Sun' },
  { name: 'Shop 3', suburb: 'Waurn Ponds', stocks: 'Full range', open: 'Wed to Sat' },
  { name: 'Shop 4', suburb: 'Waurn Ponds', stocks: 'Full range', open: 'Daily' },
  { name: 'Shop 5', suburb: 'Waurn Ponds', stocks: 'Full range', open: 'Thu to Sun' }
]

const faqs = [
  {
    question: 'Is it safe for sensitive skin?',
    answer: 'The toner and moisturizer are the gentlest. Patch test the serum on your jaw for two nights before using it on your face, because the niacinamide can sting if your barrier is already irritated.'
  },
  {
    question: 'How long does a bottle last?',
    answer: 'About eight weeks if you use it twice a day. The serum lasts longer because three drops is all you need.'
  },
  {
    question: 'Why is there no plastic wrap?',
    answer: 'We ship in cardboard with paper tape. Nothing in the box needs to go in the bin, it can all go in the recycling.'
  },
  {
    question: 'Do you test on animals?',
    answer: 'No, and we never have. Everything is tested on us and on volunteers who put their hand up at the markets.'
  }
]
</script>

<style scoped>
.contact-card p {
  margin-bottom: 0.2rem;
}
</style>
