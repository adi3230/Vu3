<script setup>
import {reactive, ref} from 'vue';
import ImageBanner from "./components/ImageBanner.vue";
import ProductOptions from "./components/ProductOptions.vue";
import ContactForm from "./components/ContactForm.vue";

const products = ref([
  {
    id: 1,
    labelId: 'pads-mini-normal',
    sku: 'VE11',
    headline: 'Einige Tropfen Urin',
    subHeadline: 'Einlagen Mini & Einlagen Normal  (je eine Einlage)',
    variants: []
  },
  {
    id: 2,
    labelId: 'pads-extra-super',
    sku: 'VE12',
    headline: 'Geringe bis mittlere Mengen Urin',
    subHeadline: 'Einlagen Extra & Einlagen Super  (je eine Einlage)',
    variants: []
  },
  {
    id: 3,
    labelId: 'pants',
    sku: '',
    headline: 'Größere Mengen Urin',
    subHeadline: 'Pants (eine Pants)',
    variants: [
      {
        id: 1,
        labelId: 'pants-size-m',
        sku: 'VP11',
        headline: 'Große M',
        subHeadline: 'EU 38-40/ Umfang  80-120 cm',
      },
      {
        id: 2,
        labelId: 'pants-size-l',
        sku: 'VP12',
        headline: 'Große L',
        subHeadline: 'EU 40-42/ Umfang  110-140 cm',
      }
    ]
  }
])
const userSelection = ref(null);
const form = reactive({
  firstName: '',
  lastName: '',
  streetName: '',
  additionalStreetInfo: '',
  postcode: '',
  city: '',
  country: '',
  email: '',
  telephone: ''
});

const sendForm = () => {
  console.log('I am clicke din child');
}

</script>

<template>
  <header>
    <div class="nav"></div>
    <div class="main-menu">
      <nav class="nav-bar">
        <div class="logo-wrapper">
          <a href="#" class="logo">
            <img src="./assets/lillydoo-logo.svg" alt="LILLYDOO LOGO">
          </a>
        </div>
      </nav>
    </div>
  </header>
  <ImageBanner :desktop-image="'./src/assets/header-home-collection-x-d.jpg'"
               :tablet-image="'./src/assets/header-home-collection-x-t.jpg'"
               :mobile-image="'./src/assets/header-home-collection-x-m.jpg'"
  />
  <div class="page-wrap">
    {{form}}
    <div class="single-sample">
      <ProductOptions v-model:selected-option="userSelection" :product-options="products"/>
      <ContactForm v-model:first-name="form.firstName"
                   v-model:last-name="form.lastName"
                   v-model:street-name="form.streetName"
                   v-model:additional-street-info="form.additionalStreetInfo"
                   v-model:postcode="form.postcode"
                   v-model:city="form.city"
                   v-model:country="form.country"
                   v-model:email="form.email"
                   v-model:telephone="form.telephone"
                   @send="sendForm"
      />
    </div>
  </div>

</template>

<style lang="scss">
h1 {
  color: $color-primary;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.nav {
  display: none;

  @include media-breakpoint-up(md) {
    display: block;
    background-color: $black;
    height: 40px;
  }
}

.nav-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  @include media-breakpoint-up(md) {
    max-width: 1287px;
    margin: 0 auto;
    justify-content: flex-start;
  }
}

.main-menu {
  height: 4.125rem;
  padding: .6rem 2rem;
  background-color: $white;

  @include media-breakpoint-up(md) {
    margin: 0 auto;
  }
}

.logo {
  display: flex;
  height: 100%;
  align-items: center;
  justify-content: center;
  width: 9.375rem;
  margin: 0 0 0 .3125rem;

  img {
    width: 100%;
  }
}

.image-banner-wrapper {
  display: flex;
  position: relative;
  padding-top: 0;
  padding-bottom: 0;
  min-height: 35.25rem;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  background-color: #f2f0ec;
}

.image-banner-wrapper__image {
  width: 100%;
  height: auto;
}

.single-sample {
  display: grid;
  grid-template-columns: minmax(0, 1fr);

  @include media-breakpoint-up(md) {
    gap: 72px;
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

  @include media-breakpoint-up(lg) {
    grid-template-columns: repeat(2, 1fr);
  }
}


</style>
