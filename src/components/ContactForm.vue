<template>
  <section class="routine-form">
    <h2>{{ formTitle }}</h2>
    <p class="section-note">
      Answer a few questions about your skin and we will send back a routine built
      from the four products, in the order to use them. It takes about a minute and
      we do not sign you up to anything.
    </p>

    <!-- submit.prevent stops the browser reloading the page, which would
         throw away everything typed in -->
    <form class="form" @submit.prevent="submitForm">
      <fieldset>
        <legend>Your skin</legend>

        <div class="form-grid">
          <!-- 1. dropdown, options come from an array with v-for -->
          <div class="field">
            <label for="skinType">Skin type</label>
            <select id="skinType" v-model="form.skinType">
              <option value="">Choose one</option>
              <option v-for="type in skinTypes" :key="type.value" :value="type.value">
                {{ type.label }}
              </option>
            </select>
            <p v-if="errors.skinType" class="field-error">{{ errors.skinType }}</p>
          </div>

          <!-- 2. number, the .number modifier stores 3 rather than "3" -->
          <div class="field">
            <label for="stepsNow">Steps in your routine now</label>
            <input type="number" id="stepsNow" min="0" max="12"
                   v-model.number="form.stepsNow">
            <p v-if="errors.stepsNow" class="field-error">{{ errors.stepsNow }}</p>
          </div>

          <!-- 3. radio group, all four share one v-model -->
          <div class="field full">
            <label id="feelLabel">How does your skin feel after cleansing?</label>
            <div class="choice-group" role="radiogroup" aria-labelledby="feelLabel">
              <label v-for="option in feelOptions" :key="option.value" class="choice">
                <input type="radio" :value="option.value" v-model="form.feel">
                {{ option.label }}
              </label>
            </div>
            <p v-if="errors.feel" class="field-error">{{ errors.feel }}</p>
          </div>
        </div>
      </fieldset>

      <fieldset>
        <legend>Your details</legend>

        <div class="form-grid">
          <!-- 4. text -->
          <div class="field">
            <label for="firstName">First name</label>
            <input type="text" id="firstName" v-model="form.firstName">
            <p v-if="errors.firstName" class="field-error">{{ errors.firstName }}</p>
          </div>

          <div class="field">
            <label for="email">Email</label>
            <input type="text" id="email" inputmode="email"
                   placeholder="name@example.com" v-model="form.email">
            <p v-if="errors.email" class="field-error">{{ errors.email }}</p>
          </div>

          <div class="field full">
            <label for="notes">Anything else we should know?</label>
            <textarea id="notes" v-model="form.notes"
                      placeholder="Allergies, products that did not agree with you, anything like that."></textarea>
          </div>
        </div>
      </fieldset>

      <!-- 5. checkbox, left unticked so nobody is signed up by accident -->
      <div class="choice-group">
        <label class="choice">
          <input type="checkbox" v-model="form.restock">
          Email me when something is back in stock
        </label>
      </div>

      <div class="form-actions">
        <button class="button" type="submit">Send my routine</button>
      </div>

      <p v-if="showSuccess" class="form-success">
        Thanks, your answers are on their way. This form will clear itself in a moment.
      </p>
    </form>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// configuration from the parent, both have a fallback so the component
// still works if it is dropped somewhere without them
const props = defineProps({
  formTitle: {
    type: String,
    default: 'Find your routine'
  },
  defaultName: {
    type: String,
    default: ''
  }
})

const emit = defineEmits(['submit-form'])

const skinTypes = [
  { value: 'dry', label: 'Dry' },
  { value: 'oily', label: 'Oily' },
  { value: 'combination', label: 'Combination' },
  { value: 'normal', label: 'Normal' },
  { value: 'sensitive', label: 'Sensitive' }
]

const feelOptions = [
  { value: 'tight', label: 'Tight and dry' },
  { value: 'oily', label: 'Oily by midday' },
  { value: 'both', label: 'Both, depending on the area' },
  { value: 'normal', label: 'Comfortable' }
]

// text, one at sign, more text, a dot, then at least two characters
const EMAIL_PATTERN = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/

// the starting state, kept in a function so the reset can reuse it
function emptyForm() {
  return {
    skinType: '',
    stepsNow: null,
    feel: '',
    firstName: props.defaultName,
    email: '',
    notes: '',
    restock: false
  }
}

const form = ref(emptyForm())
const errors = ref({})
const showSuccess = ref(false)

function validate() {
  const found = {}

  if (form.value.skinType === '') {
    found.skinType = 'Choose the option closest to your skin.'
  }

  if (form.value.stepsNow === null || form.value.stepsNow === '') {
    found.stepsNow = 'Tell us how many steps you use now, 0 is a valid answer.'
  } else if (form.value.stepsNow < 0 || form.value.stepsNow > 12) {
    found.stepsNow = 'Enter a number between 0 and 12.'
  }

  if (form.value.feel === '') {
    found.feel = 'Pick the one that sounds most like your skin.'
  }

  if (form.value.firstName.trim() === '') {
    found.firstName = 'We need a first name to address the routine to.'
  }

  if (form.value.email.trim() === '') {
    found.email = 'We send the routine by email, so we need an address.'
  } else if (!EMAIL_PATTERN.test(form.value.email.trim())) {
    found.email = 'That does not look like an email address.'
  }

  errors.value = found
  return Object.keys(found).length === 0
}

function submitForm() {
  if (!validate()) {
    showSuccess.value = false
    return
  }

  // a shallow copy, so clearing the fields below cannot empty the card the
  // parent is holding
  emit('submit-form', { ...form.value })

  showSuccess.value = true

  // the fields clear on their own two seconds later, which leaves the
  // success message on screen long enough to be read
  setTimeout(() => {
    form.value = emptyForm()
    errors.value = {}
    showSuccess.value = false
  }, 2000)
}
</script>

<style scoped>
/* the form card and grid come from styles.css, these are the bits that
   only this component needs */
fieldset {
  border: 0;
}

/* the text style controls fill their column, but a radio or a checkbox
   must not, or the label text is pushed onto the next line */
.field select,
.field textarea,
.field input:not([type="radio"]):not([type="checkbox"]) {
  width: 100%;
}

/* .field label sets display block for the field labels, so the choice
   labels need putting back onto one line with their button */
.field .choice {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-weight: normal;
  margin-bottom: 0;
}
</style>
