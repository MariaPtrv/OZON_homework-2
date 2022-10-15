<template>
  <div class="info">

    <div class="info-column">
      <h5 class="info-title">Заявка:</h5>
      <h5 class="info-value">{{candidate.ticket}}</h5>

      <h5 class="info-title">Логин:</h5>
      <h5 class="info-value">{{candidate.login}}</h5>
    </div>

    <div class="info-column">
      <h5 class="info-title">Дата выхода:</h5>
      <h5 class="info-value">{{getShortDate(candidate.employmentDate) }}</h5>

      <h5 class="info-title">Дата оформления:</h5>
      <h5 class="info-value">{{getShortDate(candidate.registeredDate)}}</h5>
    </div>

    <div class="info-column">
      <h5 class="info-title">Статус ФП:</h5>
      <status-component :is-status-success="FPStatus.isSuccess"
                        :status-label="FPStatus.label"></status-component>
      <h5 class="info-title">Статус УЗ:</h5>
      <status-component :is-status-success="accountStatus.isSuccess"
                        :status-label="accountStatus.label"></status-component>
    </div>
  </div>
</template>

<script>
import StatusComponent from "@/components/customizedComponents/StatusComponent";

export default {
  name: "CandidateApplicationInfo",
  components: {StatusComponent},
  props: {
    candidate: {
      required: true
    }
  },
  computed: {
    accountStatus() {
        return {
          label: this.candidate.accountStatus === 'active' ? 'Активна' : 'Не активна',
          isSuccess: this.candidate.accountStatus === 'active'
        }
    },
    FPStatus() {
        return {
          label: this.candidate.FPStatus === 'active' ? 'Обновлено' : 'Не обновлено',
          isSuccess: this.candidate.FPStatus === 'active'
        }
    },
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
.info {
  margin-top: var(--offset-6xl);
  display: flex;
  flex-direction: row;
  row-gap: var(--offset-m);
  margin-bottom: var(--offset-3xl);
  margin-left: -24px;
}

.info-column {
  display: grid;
  grid-template-columns: repeat(2, max-content);
  grid-template-rows:  repeat(2, var(--offset-6xl));
  align-items: center;
  row-gap: var(--offset-m);
  column-gap: var(--offset-m);
  padding: 0 24px;
  border-right: 1px solid var(--border-color);
}

.info :last-of-type {
  border-right: none;
}


.info-column > .status-success {
  background: transparent;
}

.info-column > .status-waiting {
  background: transparent;
}

.info-title {
  font-weight: 400;
  line-height: 16px;
  color: var(--black-color-text);
}
</style>