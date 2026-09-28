<template>
  <div id="app-layout">
    <AppHeader :active-view="activeView" @navigate="showView" />

    <main>
      <!-- only the chosen view is on the page at a time -->
      <HomeView v-if="activeView === 'home'" @navigate="showView" />
      <ProductsView v-else-if="activeView === 'products'" />

      <template v-else>
        <ContactView />

        <section class="routine-wrap">
          <ContactForm
            form-title="Find your routine"
            :default-name="defaultName"
            @submit-form="handleFormSubmit"
          />

          <!-- stays on screen after the child clears itself, because this
               data lives up here and not in the form -->
          <div v-if="acknowledgement" class="ack-card">
            <h3>Thanks {{ acknowledgement.firstName }}, we have your answers</h3>
            <p>
              Nothing has been sent anywhere. This is what you told us, and we will
              email your routine to
              <strong>{{ acknowledgement.email }}</strong> within two working days.
            </p>
            <ul>
              <li><strong>Skin type:</strong> {{ skinTypeLabels[acknowledgement.skinType] }}</li>
              <li><strong>Steps in your routine now:</strong> {{ acknowledgement.stepsNow }}</li>
              <li><strong>After cleansing:</strong> {{ feelLabels[acknowledgement.feel] }}</li>
              <li v-if="acknowledgement.notes">
                <strong>Notes:</strong> {{ acknowledgement.notes }}
              </li>
              <li><strong>Restock emails:</strong> {{ acknowledgement.restock ? 'Yes' : 'No' }}</li>
            </ul>
          </div>
        </section>
      </template>
    </main>

    <AppFooter @navigate="showView" />
  </div>
</template>

<script setup>
import { ref } from 'vue'

import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import HomeView from './components/HomeView.vue'
import ProductsView from './components/ProductsView.vue'
import ContactView from './components/ContactView.vue'
import ContactForm from './components/ContactForm.vue'

// which page is showing, changed by the header and footer nav
const activeView = ref('home')

// passed down to the form as a starting value
const defaultName = ref('')

// null until the form is submitted, which is what the v-if is testing
const acknowledgement = ref(null)

// the payload carries the stored values, these turn them back into the
// wording the user actually saw on the form
const skinTypeLabels = {
  dry: 'Dry',
  oily: 'Oily',
  combination: 'Combination',
  normal: 'Normal',
  sensitive: 'Sensitive'
}

const feelLabels = {
  tight: 'Tight and dry',
  oily: 'Oily by midday',
  both: 'Both, depending on the area',
  normal: 'Comfortable'
}

function showView(pageId) {
  activeView.value = pageId
  window.scrollTo(0, 0)
}

// runs when the child emits submit-form, the payload is the shallow copy
function handleFormSubmit(submitted) {
  acknowledgement.value = submitted
}
</script>

<style>
#app-layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1;
}

.routine-wrap {
  padding-top: 0;
}
</style>
