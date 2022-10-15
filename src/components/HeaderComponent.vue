<template>
  <header>
    <a href="" class="logo">
      <img src="../assets/logo.svg" alt="logo">
      <h4>HR</h4>
    </a>
    <h5 class="logout">Выйти</h5>
    <nav>
      <a v-for="option in options" :key="option.name"
         :class="{'nav-selected': isSelected(option)}"
         @click="selectOption(option.name)">
        {{ option.label }}
      </a>
    </nav>
  </header>
</template>

<script>
export default {
  name: "HeaderComponent",
  props: {
    options: {
      required: true,
      default: [
        {
          label: 'Все',
          name: 'all'
        },
        {
          label: 'Ожидают загрузки',
          name: 'only-waiting'
        },
        {
          label: 'Загружены кандидатом',
          name: 'only-loaded'
        },
      ]
    },
    selectedFilter: {
      required: false,
      default: 0
    }
  },
  computed: {
    selectedOptionIndex() {
      return this.selectedFilter;
    }
  },
  methods: {
    selectOption(name) {
      this.$emit('filterIndex', this.options.findIndex((option) => option.name === name))
    },
    isSelected(option) {
      const optionId = this.options.findIndex((item) => item.name === option.name);
      return optionId === this.selectedOptionIndex;
    }
  }
}
</script>

<style scoped>
/* header */
header {
  height: var(--header-height);
  box-sizing: border-box;
  padding: 0 32px;

  display: grid;
  justify-items: start;
  grid-template-columns: auto 47px;
  grid-template-rows: 56px var(--offset-large);

  border-bottom: var(--offset-xs) solid var(--border-color);
  background: var(--main-white-color);
}

/* header -> logo section */
.logo {
  display: flex;
  flex-direction: row;
  align-items: center;
  column-gap: var(--offset-l);
}

/* header -> logout */
.logout {
  padding-top: var(--offset-5xl);
}

/* header -> nav */
nav {
  display: flex;
  flex-direction: row;
  column-gap: 32px;
  align-items: center;
}

/* header -> nav -> nav item */
a {
  font-style: normal;
  font-weight: 400;
  font-size: var(--offset-4xl);
  line-height: var(--offset-6xl);
  color: var(--black-color-text);
  text-decoration: none;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

a::after {
  content: " ";
  position: relative;
  top: var(--offset-l);
  display: block;
  width: 100%;
  height: var(--offset-xs);
  background: transparent;
  border: var(--offset-xxs) solid transparent;
  border-radius: var(--offset-s);
  box-sizing: border-box;
}

.nav-selected {
  color: var(--black-color-header);
  transition: 15ms all;
}

.nav-selected::after {
  background: var(--blue-color-text);
  border-color: var(--blue-color-text);
}
</style>