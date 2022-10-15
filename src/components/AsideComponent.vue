<template>
  <aside>
    <section class="search-block">
        <input-component type="search" placeholder="Поиск"
                         @update-search="handleSearch"></input-component>
        <button></button>
    </section>

    <CandidateItem v-for="candidate in filterCandidates" :key="candidate.id"
                   :candidate=candidate
                   :is-status-success="candidate.FPStatus === 'active'"
                   @click="$emit('selectCandidate', candidate.id)"
    ></CandidateItem>
  </aside>
</template>

<script>
import InputComponent from "@/components/customizedComponents/InputComponent";
import CandidateItem from "@/components/candidatesItem/CandidateItem";

export default {
  name: "AsideComponent",
  components: {
    InputComponent,
    CandidateItem
  },
  props: {
    candidatesList: {
      required: true
    },
    headerFilterValue: {
      required: false,
      default: 'all'
    }
  },
  data() {
    return {
      searchValue: '',
      filterDecoder: {
        'only-waiting': 'idle',
        'only-loaded': 'success'
      }
    }
  },
  computed: {
    filterCandidates() {
      if (this.headerFilterValue !== 'all') {
        return this.candidatesList.filter((candidate) =>
            this.getCandidateFullName(candidate).includes(this.searchValue.toLowerCase()) &&
            candidate.applicationStatus === this.filterDecoder[this.headerFilterValue]);
      } else
        return this.candidatesList.filter((candidate) =>
            this.getCandidateFullName(candidate).includes(this.searchValue.toLowerCase()));
    }
  },
  methods: {
    getCandidateFullName(candidate) {
      return candidate.middleName.toLowerCase() + ' '
          + candidate.firstName.toLowerCase() + ' '
          + candidate.lastName.toLowerCase();
    },
    handleSearch(s) {
      this.searchValue = s;
    },
    handleSelectedCandidate(id) {
      this.$emit('selectCandidate', id);
    }
  }
}
</script>

<style scoped>
aside {
  height: fit-content;
  width: var(--aside-width);
  border-radius: var(--offset-m);
  border: var(--offset-xxs) solid var(--main-white-color);
  background: var(--main-white-color);
}
button {
  padding: var(--offset-xl);
  margin-left: var(--offset-5xl);
  gap: var(--offset-m);
  box-sizing: border-box;
  width: var(--offset-large);
  height: var(--offset-large);
  background-color: var(--border-color);
  background-image: url("../assets/filter.svg");
  background-position: center;
  background-repeat: no-repeat;
  border: var(--offset-xxs) solid transparent;
  border-radius: var(--offset-m);
  outline: none;
}

.search-block {
  height: 76px;
  width: 100%;
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  padding-top: var(--offset-5xl);
}

</style>