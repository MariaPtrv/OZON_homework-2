<template>
  <header-component v-if="isLoaded"
                    :selectedFilter="selectedFilterHeaderIndex"
                    :options="headerFilterOptions"
                    @filter-index="handleFilter"
  ></header-component>
  <section class="content" v-if="isLoaded">
    <aside-component :candidates-list="currentData" @select-candidate="handleSelectedCandidate"
                     :header-filter-value="headerFilterOptions[selectedFilterHeaderIndex].name"></aside-component>
    <candidate-card :candidate="selectedCandidate"
                    @newState="handleNewStateEmit"
                    @changeGenderById="handleChangeGender"
                    @changeSelectedCitizenship="handleChangeCitizenship"></candidate-card>
  </section>

</template>

<script>
import AsideComponent from "@/components/AsideComponent";
import CandidateCard from "@/components/candidateInfo/CandidateCard";
import HeaderComponent from "@/components/HeaderComponent";

export default {
  name: "mainPage",
  components: {
    HeaderComponent,
    CandidateCard,
    AsideComponent
  },
  created() {
    this.getData();
  },
  data() {
    return {
      data: [],
      selectedCandidateId: 0,
      headerFilterOptions: [
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
      ],
      selectedFilterHeaderIndex: 0
    }
  },
  computed: {
    isLoaded() {
      return this.data.length > 0;
    },
    currentData: {
      get() {
        return this.data;
      },
      set(newValue) {
        this.data = newValue
      }
    },
    selectedCandidate() {
      return this.currentData.find((candidate) => candidate.id == this.selectedCandidateId);
    }
  },
  methods: {
    handleSelectedCandidate(id) {
      this.selectedCandidateId = id;
    },
    handleFilter(index) {
      this.selectedFilterHeaderIndex = index
    },
    async getData() {
      const response = await fetch('/mock.json');
      const data = await response.json();
      data.forEach((candidate) => candidate.fullName = this.getFullName(candidate))
      this.data = data;
      this.selectedCandidateId = data[0].id;
    },
    getFullName(candidate) {
      return candidate.lastName + ' ' + candidate.firstName + ' ' + candidate.middleName;
    },
    handleNewStateEmit(newStateCandidate) {
      this.currentData = this.data.map((candidate) => {
        if (candidate.id === newStateCandidate.id) {
          newStateCandidate.fullName = this.getFullName(newStateCandidate);
          return newStateCandidate;
        } else return candidate;
      });
    },
    handleChangeGender(id) {
      this.currentData.map((candidate) => {
        if (candidate.id == id) {
          candidate.gender === 'male' ? candidate.gender = 'female' : candidate.gender = 'male'
        }
      });
    },
    handleChangeCitizenship(newValue) {
      this.currentData.map((candidate) => {
        if (candidate.id == newValue.id)
          candidate.citizenship = newValue.citizenship;
      });
    }
  },
}
</script>

<style scoped>
/* all page under header */
.content {
  height: 100vh;
  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: var(--offset-5xl);
  padding: var(--offset-5xl) 0;
  box-sizing: border-box;
}
</style>