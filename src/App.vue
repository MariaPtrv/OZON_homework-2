<template>
  <main-page></main-page>
</template>

<script>

import MainPage from "@/pages/mainPage";

export default {
  name: 'App',
  components: {
    MainPage
  }
}
</script>
<style>
@import './assets/styles/normalize.css';
</style>
<style>
/* fonts */
@font-face {
  font-family: 'Inter';
  src: url('./fonts/Inter-Medium.ttf') format('woff2');
  font-style: normal;
  font-weight: 400;
  font-size: 15px;
}

/* css variables */
#app {
  --main-color: #F9FAFB;
  --main-white-color: #FFFFFF;
  --black-color-header: rgba(0, 17, 34, 0.95);
  --black-color-text: rgba(0, 17, 34, 0.66);
  --blue-color-text: #005BFF;
  --border-color: rgba(97, 131, 162, 0.16);
  --success-color: rgba(29, 174, 64, 0.12);
  --waiting-color: rgba(247, 178, 0, 0.12);
  --background-input: rgba(97, 131, 162, 0.1);
  --background-input-light: rgba(97, 131, 162, 0.05);
  --black-color-text-light: rgba(0, 17, 34, 0.36);
  --input-value-color: rgba(13, 29, 45, 255);

  --waiting-indicator-color: #F7B200;
  --success-indicator-color: #1DAE40;

  --offset-xxs: 1px;
  --offset-xs: 2px;
  --offset-default: 4px;
  --offset-s: 5px;
  --offset-m: 8px;
  --offset-l: 9px;
  --offset-xl: 10px;
  --offset-xxl: 12px;
  --offset-3xl: 14px;
  --offset-4xl: 15px;
  --offset-5xl: 16px;
  --offset-6xl: 24px;
  --offset-large: 44px;

  --input-width-city: 968px;
  --header-height: 100px;
  --aside-width: 336px;

  --candidate-info-width: 1016px;
  --search-input-width: 244px;
  --search-icon-top: 30px;

  font-family: 'Inter';
  background: var(--main-color);
}


h2 {
  font-family: Inter;
  font-weight: 600;
  font-size: var(--offset-6xl);
  line-height: 32px;
  margin: 0 0 var(--offset-xl) 0;
  padding: 0;
  color: var(--black-color-header);
}

h4 {
  font-family: Inter;
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 28px;
  margin: 0;
  padding: 0;
  color: var(--black-color-header);
}

h6 {
  font-family: Inter;
  font-size: 13px;
  font-style: normal;
  font-weight: 400;
  line-height: 20px;
  margin: 0;
  padding: 0;
  color: var(--black-color-header);
}

h5 {
  font-family: Inter;
  font-size: var(--offset-4xl);
  font-weight: 400;
  font-style: normal;
  text-align: left;
  line-height: var(--offset-6xl);
  margin: 0;
  padding: 0;
  color: var(--black-color-header);
}

.text-secondary {
  color: var(--black-color-text);
}

.text-bold {
  font-weight: 600;
}

</style>
