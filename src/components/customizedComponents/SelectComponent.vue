<template>
  <label class="info-title">{{label}}</label>
  <select :name="id" id="citizenship" @change="$emit('changeSelected', $event.target.value)" :value="selected">
    <option :value="option.value" v-for="option in options" :key="option.value">{{option.label}}</option>
  </select>
</template>

<script>
export default {
  name: "SelectComponent",
  props: {
    selected: {
      type: String,
      required: false
    },
    options: {
      type: Array,
      required: true
    },
    label: {
      type: String,
      required: true
    },
    id: {
      type: String,
      required: true
    }
  },
}
</script>

<style scoped>
label {
  font-size: 13px;
  font-style: normal;
  margin: 0;
  padding: 0;
  font-weight: 400;
  line-height: 16px;
  color: var(--black-color-text);
}
select {
  width: 100%;
  height: var(--offset-large);
  background: var(--background-input);
  border: var(--offset-xxs) solid transparent;
  border-radius: var(--offset-m);
  padding: 6px var(--offset-xxl);
  outline: none;
  appearance: none;
  background-image: url("../../assets/arrow.svg");
  background-position: calc(100% - 18px) center;
  background-repeat: no-repeat;
  color: var(--input-value-color);
  box-sizing: border-box;
  font-weight: 400;
  font-size: var(--offset-4xl);
  line-height: var(--offset-5xl);
}

.city-input :last-child {
  width: var(--input-width-city);
  background-color: var(--background-input-light);
  color: var(--black-color-text-light);
}
</style>