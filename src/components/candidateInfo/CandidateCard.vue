<template>
  <article class="selected-candidate-info">
    <section class="candidate-info">
      <h2>{{ candidate.fullName }}</h2>
      <status-component :is-status-success="applicationStatus.isSuccess"
                        :status-label="applicationStatus.label"></status-component>
      <candidate-application-info :candidate="candidate"></candidate-application-info>
    </section>
    <candidate-personal-info
        :candidate="candidate"
        @newState="handleNewStateEmit"
        @changeGenderById="handleChangeGender"
        @changeSelectedCitizenship="handleSelectedCitizenship"></candidate-personal-info>
  </article>
</template>

<script>
import CandidateApplicationInfo from "@/components/candidateInfo/parts/CandidateApplicationInfo";
import CandidatePersonalInfo from "@/components/candidateInfo/parts/CandidatePersonalInfo";
import StatusComponent from "@/components/customizedComponents/StatusComponent";

export default {
  name: "CandidateCard",
  components: {StatusComponent, CandidatePersonalInfo, CandidateApplicationInfo},
  props: {
    candidate: {
      required: true
    }
  },
  computed: {
    applicationStatus() {
      return {
        label: this.candidate.applicationStatus === 'success' ? 'Загружена кандидатом' : 'Ожидают загрузки',
        isSuccess: this.candidate.applicationStatus === 'success'
      }
    }
  },
  methods: {
    handleNewStateEmit(newState) {
      this.$emit('newState', newState);
    },
    handleChangeGender(id) {
      this.$emit('changeGenderById', id)
    },
    handleSelectedCitizenship(newValue) {
      this.$emit('changeSelectedCitizenship', newValue);
    }
  }
}
</script>

<style scoped>
.selected-candidate-info {
  width: var(--candidate-info-width);
  height: fit-content;
  box-sizing: border-box;
  padding: var(--offset-6xl) var(--offset-6xl) var(--offset-5xl) var(--offset-6xl);
  background: var(--main-white-color);
  border-radius: var(--offset-m);
}
</style>