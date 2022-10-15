<template>
  <h6 class="info-title">{{ title }}</h6>
  <div class="info-sex">
    <radio-btn v-for="item in options" :key="item.value"
               :label="item.label"
               :name="item.name"
               :value="item.value"
               :is-checked="item.isChecked"
               @stateChanged="handleRadioBtnClick"
    ></radio-btn>
  </div>
</template>

<script>
import RadioBtn from "@/components/customizedComponents/RadioBtn";

export default {
  name: "RadioBtnGroup",
  components: {RadioBtn},
  props: {
    title: {
      type: String,
      required: true
    },
    options: {
      required: true,
      default: [
        {label: 'Да', name: 'name', value: 'value1'},
        {label: 'Нет', isChecked: true, name: 'name', value: 'value1'}]
    }
  },
  methods: {
    handleRadioBtnClick(state) {
      const newOptionState = JSON.parse(JSON.stringify(this.options));
      newOptionState.map((option) => {
        if (option.value == state.value) {
          option.isChecked = state.checked
        } else option.isChecked = false
      });
      this.$emit('newOptionsState', newOptionState);
    }
  }
}
</script>

<style scoped>
.info-sex {
  display: flex;
  width: 306.67px;
  flex-direction: row;
  justify-content: space-between;
}

.info-title {
  font-size: 13px;
  font-style: normal;
  margin: 0;
  padding: 0;
  font-weight: 400;
  line-height: 16px;
  color: var(--black-color-text);
}
</style>