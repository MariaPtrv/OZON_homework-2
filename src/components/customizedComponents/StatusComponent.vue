<template>
  <div class="status" :class="[isStatusSuccess ? 'status-success' :'status-waiting', withoutBackground]">
    <h6 class="text-bold">{{statusLabel}}</h6>
  </div>
</template>

<script>
export default {
  name: "StatusComponent",
  props: {
    isStatusSuccess: {
      type: Boolean,
      required: true
    },
    statusLabel: {
      type: String,
      required: true
    },
    withoutBackground: {
      type: Boolean,
      required: false,
      default: true
    }
  }
}
</script>

<style scoped>
.status {
  display: flex;
  flex-direction: row;
  align-items: center;
  height: var(--offset-6xl);
  border-radius: var(--offset-5xl);
  width: fit-content;
  box-sizing: border-box;
}

.status-waiting {
  background: var(--waiting-color);
  padding: var(--offset-xs) var(--offset-xxl) var(--offset-xs) var(--offset-default);
}

.status-waiting ::before {
  content: '';
  width: 6px;
  height: 6px;
  box-sizing: border-box;
  position: relative;
  display: inline-block;
  margin: 0 5px 2px 9px;
  border: 1px solid var(--waiting-indicator-color);
  border-radius: 50%;
  background: var(--waiting-indicator-color);
}

.status-success {
  background: var(--success-color);
  padding: var(--offset-xs) var(--offset-xxl) var(--offset-xs) var(--offset-default);
}

.status-success ::before {
  content: '';
  width: 6px;
  height: 6px;
  box-sizing: border-box;
  position: relative;
  display: inline-block;
  margin: 0 5px 2px 9px;
  border: 1px solid var(--success-indicator-color);
  border-radius: 50%;
  background: var(--success-indicator-color);
}

.withoutBackground {
  background: transparent;
}
</style>