<template>
  <img src="../../assets/search.svg" alt="search icon" class="search-icon" v-if="type==='search'">
  <input :placeholder=placeholder class="search-input" type="search" v-model="searchInput"
         @input="$emit('updateSearch', searchInput)" v-if="type==='search'">

  <label  v-if="label!==undefined">{{ label }}</label>
  <input :type=type
         :value="modelValue"
         :disabled=isDisabled
         :class="{'large-width': isLargeWidth}"
         @input="$emit('update:modelValue', $event.target.value)"
         v-if="type==='text'  || type==='date'"/>
</template>

<script>
export default {
  name: "InputComponent",
  props: {
    label: {
      type: String,
      required: false,
    },
    modelValue: {
      type: String,
      required: false,
    },
    type: {
      type: String,
      required: false,
      default: "text"
    },
    isDisabled: {
      type: Boolean,
      required: false,
      default: false
    },
    isLargeWidth: {
      type: Boolean,
      required: false,
      default: false
    },
    placeholder: {
      type: String,
      required: false,
    }
  },
  data() {
    return {
      searchInput: ''
    }
  }
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

input {
  height: var(--offset-large);
  outline: none;
  box-sizing: border-box;
  background: var(--background-input);
  border: var(--offset-xxs) solid transparent;
  border-radius: var(--offset-m);
  color: var(--input-value-color);
  padding: var(--offset-3xl) var(--offset-xxl);
  font-weight: 400;
  font-size: var(--offset-4xl);;
  line-height: var(--offset-5xl);
}

input[value] {
  color: var(--input-value-color);
  font-size: 15px;
}

input[disabled] {
  color: var(--black-color-text);
}

input[type='text'], input[type='date'] {
  width: 306.66px;
  height: var(--offset-large);
  font-family: 'Inter';
}

input::-webkit-calendar-picker-indicator {
  background: url("../../assets/calendar-light.svg") no-repeat;
  background-size: contain;
}

.large-width {
  width: var(--input-width-city) !important;
  background-color: var(--background-input-light) !important;
  color: var(--black-color-text-light) !important;
}

input[value] {
  color: var(--input-value-color);
  font-size: 15px;
}

input[disabled] {
  color: var(--black-color-text);
}

.search-input {
  box-sizing: border-box;
  padding-left: var(--offset-large);
  width: var(--search-input-width);
}

.search-icon {
  position: relative;
  display: inline;
  width: 19px;
  height: 19px;
  top: var(--offset-xxl);
  left: 35px;
}

.search-input::-webkit-search-cancel-button {
  -webkit-appearance: none;
}
</style>