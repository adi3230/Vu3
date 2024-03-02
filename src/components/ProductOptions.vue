<script setup>

import {ref} from "vue";

const selectedOption = ref(null);
const props = defineProps({
  productOptions: {
    type: Array,
    required: true
  }
})
const emits = defineEmits(['update:selected-option'])

const updateSelectedOption = (v, o) => {
  if (v.variants && v.variants.length > 0) {
    // If a parent radio button is selected, select the first nested radio button
    emits('update:selected-option', v.variants[0]);
    // Set the selectedOption to the first nested radio button
    selectedOption.value = v.variants[0].labelId;
  } else {
    emits('update:selected-option', v);
  }
}
const isOptionSelected = (option) => {
  return selectedOption.value === option.labelId ||
      (option.variants && option.variants.some(variant => variant.labelId === selectedOption.value));
}

</script>

<template>
<div class="product-options">
  <h2 class="product-options__headline">1. Wähle Deine Produkte</h2>
  <template v-for="option in props.productOptions" :key="option.id">
    <label for="option.sku"
           class="product-options__option"
           :class="{ 'selected': isOptionSelected(option) }"
    >
      <input type="radio"
             :name="option.labelId"
             :id="option.sku"
             :value="option.labelId"
             v-model="selectedOption"
             @change="updateSelectedOption(option)"
      />
      <div class="option-content">
        <span>{{ option.headline }}</span>
        <span>{{ option.subHeadline }}</span>
      </div>
      <ul v-if="option.variants.length > 0" class="product-options__variants">
        <li v-for="variant in option.variants" :key="variant.id">
          <label for="variant.sku"
                 class="product-options__option"
          >
            <input type="radio"
                   :name="variant.labelId"
                   :id="variant.sku"
                   :value="variant.labelId"
                   v-model="selectedOption"
                   @change="updateSelectedOption(variant, option)"
            />
            <div class="option-content">
              <span>{{ option.headline }}</span>
              <span>{{ option.subHeadline }}</span>
            </div>
          </label>
        </li>
      </ul>
    </label>
  </template>
</div>
</template>

<style scoped>
.product-options {
  display: flex;
  flex-direction: column;
}

.product-options__option {
  height: 123px;
  background-color: #F8F5F1;
  margin: 10px;
  border: 2px solid transparent;
  position: relative;
  transition: border .3s ease-in-out;
}

.product-options__option:hover {
  cursor: pointer;
}

.product-options__option input[type="radio"] {
  position: absolute;
  opacity: 0;
}

.product-options__option input[type="radio"]:checked + .option-content {
  font-weight: bold;
}

.product-options__variants {
  margin-left: 25px;
  list-style: none;
}

.selected {
  /* Add your styling for the selected option here */
  border: 2px solid #194E4F;
  /* Example: Green border for the selected option */

  &:before, &:after {
    content: '';
    position: absolute;
    border-color: transparent;
    border-style: solid;
  }

  &:before {
    border-radius: 0;
    border-width: 28px;
    border-right-color: #194E4F;
    border-top-color: #194E4F;
    right: 0;
  }

  &:after {
    content: '';
    display: inline-block;
    transform: rotate(45deg);
    height: 15px;
    width: 9px;
    border-bottom: 2px solid #FFFFFF;
    border-right: 2px solid #FFFFFF;
    right: 11px;
    top: 1px;
  }
}


</style>