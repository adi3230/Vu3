<script setup>
import {ref} from "vue";

const emit = defineEmits(['send'])

const firstName = ref('');
const lastName = ref('');
const streetName = ref('');
const additionalStreetInfo = ref('');
const postcode = ref('');
const city = ref('');
const country = ref('');
const email = ref('');
const telephone = ref('');

const sendFormDetails = (event) => {
emit('send');
};

</script>

<template>
<div class="contact-form">
  <h2 class="contact-form__headline">
    2. Versandadresse
  </h2>
  <div class="contact-form__address">
    <div class="contact-form__field-group">
      <input type="text"
             id="firstName"
             v-model="firstName"
             @input="$emit('update:first-name', $event.target.value)"
             autofocus required
      >
      <label class="contact-form__label" for="firstName">
        Vorname
      </label>
    </div>
    <div class="contact-form__field-group">
      <input type="text"
             id="lastName"
             v-model="lastName"
             @input="$emit('update:last-name', $event.target.value)"
             autofocus required
      >
      <label class="contact-form__label" for="lastName">
        Nachname
      </label>
    </div>
    <div class="contact-form__field-group">
      <input type="text"
             id="streetName"
             v-model="streetName"
             @input="$emit('update:street-name', $event.target.value)"
             autofocus required
      >
      <label class="contact-form__label" for="streetName">
        Straße und Hausnummer*
      </label>
    </div>
    <div class="contact-form__field-group">
      <input type="text"
             id="additionalStreetInfo"
             v-model="additionalStreetInfo"
             @input="$emit('update:additional-street-info', $event.target.value)"
             autofocus required
      >
      <label class="contact-form__label" for="streetName">
        Addresszusatz
      </label>
    </div>
    <div class="contact-form__field-group">
      <input type="text"
             id="postcode"
             v-model="postcode"
             @input="$emit('update:postcode', $event.target.value)"
             autofocus required
      >
      <label class="contact-form__label" for="postcode">
        PLZ
      </label>
    </div>
    <div class="contact-form__field-group">
      <input type="text"
             id="city"
             v-model="city"
             @input="$emit('update:city', $event.target.value)"
             autofocus required
      >
      <label class="contact-form__label" for="city">
        Stadt
      </label>
    </div>
    <div class="contact-form__field-group">
      <input type="text"
             id="country"
             v-model="country"
             @input="$emit('update:country', $event.target.value)"
             autofocus required
      >
      <label class="contact-form__label" for="country">
        Land
      </label>
    </div>
    <div class="contact-form__field-group">
      <input type="text"
             id="email"
             v-model="email"
             @input="$emit('update:email', $event.target.value)"
             autofocus required
      >
      <label class="contact-form__label" for="email">
        E-mail
      </label>
    </div>
    <div class="contact-form__field-group">
      <input type="text"
             id="telephone"
             v-model="telephone"
             @input="$emit('update:telephone', $event.target.value)"
             autofocus required
      >
      <label class="contact-form__label" for="telephone">
        Telefone
      </label>
    </div>
  </div>
  <button class="contact-form__cta" @click="sendFormDetails">JETZT KOSTENLOSE BESTELLEN</button>
</div>
</template>

<style scoped>
.contact-form__field-group {
  position: relative;
  margin-top: 32px;
  margin-bottom: 25px;

  input {
    height: 48px;
    width: 100%;
  }

  input:focus ~ .contact-form__label,
  input:not(:focus):valid ~ .contact-form__label {
    top: -15px;
    bottom: 0px;
    left: 0px;
    font-size: 11px;
    opacity: 1;
    color: #404040;
  }

}

.contact-form__label {
  font-size: 13px;
  color: #cccccc;
  position: absolute;
  top: 5px;
  left: 8px;
  transition: all 0.1s ease;
}

.contact-form__cta {
  width: 100%;
  height: 50px;
  background-color: #FF5F04;
  color: #FFFFFF;
}

</style>