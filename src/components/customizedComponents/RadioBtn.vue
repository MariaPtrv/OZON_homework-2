<template>
  <div class="container">
    <input type="radio"
           :name="name" :value="value"
           :id="value"
           :checked="isChecked"
           @change="$emit('stateChanged',{value: value, checked: $event.target.checked})">
    <label :for="value">{{ label }}</label>
  </div>
</template>

<script>
export default {
  name: "RadioBtn",
  props: {
    label: {
      type: String,
      required: true
    },
    isChecked: {
      required: false,
      default: false
    },
    name: {
      type: String,
      required: true
    },
    value: {
      type: String,
      required: true
    },
  }
}
</script>

<style scoped>
.container {
  height: var(--offset-large);
  flex-basis: 148px;
  box-sizing: border-box;
  border: var(--offset-xxs) solid var(--border-color);
  border-radius: 8px;
  padding: var(--offset-3xl) var(--offset-xxl);

  display: flex;
  flex-direction: row;
  align-items: center;

}

label {
  font-size: 13px;
  font-style: normal;
  margin: 0;
  padding: 0;
  font-weight: 400;
  line-height: 16px;
  color: var(--black-color-text);
}

input[type='radio'] {
  appearance: none;
  height: 20px;
  width: 20px;
  box-sizing: border-box;
  background-color: var(--main-white-color);
  border: 1px solid var(--border-color);
  border-radius: 50%;
  margin-right: var(--offset-m);
  display: flex;
  justify-content: center;
}

input[type='radio']:checked {
  background-color: var(--blue-color-text);
  border: 1px solid var(--blue-color-text);
}

input[type='radio']:checked::before {
  content: '';
  height: 8px;
  width: 8px;
  position: relative;
  display: inline-block;
  box-sizing: border-box;
  background-color: var(--main-white-color);
  border: 1px solid var(--main-white-color);
  border-radius: 50%;
  align-self: center;
}

input[type='radio'] + label {
  display: inline-block;
  cursor: pointer;
  user-select: none;
  font-weight: 400;
  font-size: 15px;
  line-height: 16px;
  color: var(--black-color-header);
}
</style>