<template>
  <div class="candidate">
    <h5 class="candidate-name">{{ currentCandidate.fullName }}</h5>
    <div class="candidate-status-date">
      <status-component :is-status-success="applicationStatus.isSuccess"
                        :status-label=applicationStatus.label></status-component>
      <section class="date-section">
        <img src="../../assets/calendar.svg" alt="calendar icon">
        <h6>{{ getShortDate(currentCandidate.registeredDate) }}</h6>
      </section>
    </div>
  </div>
</template>

<script>
import StatusComponent from "@/components/customizedComponents/StatusComponent";

export default {
  name: "CandidateItem",
  components: {StatusComponent},
  props: {
    candidate: {
      required: true,
    },
    isStatusSuccess: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      statusErrorLabel: 'Ожидают загрузки',
      statusSuccessLabel: 'Загружена кандидатом'
    }
  },
  computed: {
    applicationStatus() {
      return {
        label: this.currentCandidate.applicationStatus === 'success' ? 'Загружена кандидатом' : 'Ожидают загрузки',
        isSuccess: this.currentCandidate.applicationStatus === 'success'
      }
    },
    currentCandidate() {
      return this.candidate;
    }
  },

  methods: {
    getShortDate(fullDate) {
      const date = new Date(fullDate);
      return new Intl.DateTimeFormat('ru').format(date);
    },
  }
}
</script>

<style scoped>
.candidate {
  height: 80px;
  padding: var(--offset-xxl) var(--offset-5xl) 0 var(--offset-5xl);
  box-sizing: border-box;
  content: '';
  border-top: var(--offset-xxs) solid var(--border-color);
  display: flex;
  flex-direction: column;
  row-gap: var(--offset-xl);
}

.candidate:hover {
  background-color: var(--background-input);
  border-color: var(--background-input);
  cursor: pointer;
}


.candidate-name {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

/* left side -> candidate's list -> box with status & date + date's icon*/
.candidate-status-date {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.date-section {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  justify-items: flex-start;
  align-items: center;
}

.date-section > img {
  width: var(--offset-3xl);
  height: var(--offset-4xl);
  margin-right: 7px;
}
</style>