<template>
  <form class="my-1" v-on:submit.prevent>
    <div>
      <label for="appleCount">Apple</label>
      <button type="button" class="m-1" v-on:click="$emit('onApplePlusMinusClick', -5)">-5</button>
      <button type="button" class="m-1" v-on:click="$emit('onApplePlusMinusClick', -1)">-1</button>
      <input
        id="appleCount"
        type="number"
        min="1"
        max="100"
        class="mx-1"
        v-model.number="orders.apple_count"
        v-on:input="$emit('onAppleCountInput', $event)"
      >
      <button type="button" class="m-1" v-on:click="$emit('onApplePlusMinusClick', 1)">+1</button>
      <button type="button" class="m-1" v-on:click="$emit('onApplePlusMinusClick', 5)">+5</button>
    </div>
    <div>
      <span>Banana Condiments</span>
      <div class="mx-5">
        <label
          class="m-1"
          v-for="condimentOption in bananaCondimentOptions"
          v-bind:key="condimentOption.value"
        >
          <input
            type="checkbox"
            v-bind:value="condimentOption.value"
            v-model="orders.banana_condiments"
          >
          {{condimentOption.name}}
        </label>
      </div>
    </div>
  </form>
</template>
<script>
const bananaCondimentOptions = [
  {
    name: "Chocolate",
    value: "chocolate"
  },
  {
    name: "Strawberry",
    value: "strawberry"
  },
  {
    name: "Flax",
    value: "flax"
  },
  {
    name: "Miso",
    value: "miso"
  },
  {
    name: "Chili",
    value: "chili"
  },
  {
    name: "Garlic",
    value: "garlic"
  },
  {
    name: "Soy Sauce",
    value: "soy_sauce"
  },
  {
    name: "Thick Soy Sauce",
    value: "thick_soy_sauce"
  },
  {
    name: "Herbal Cream",
    value: "herbal_cream"
  }
];
export default {
  props: {
    orders: {
      type: Object,
      required: true,
      default() {
        return {
          banana_condiments: {}
        };
      }
    }
  },
  data() {
    return {
      bananaCondimentOptions: bananaCondimentOptions
    };
  }
};
</script>

