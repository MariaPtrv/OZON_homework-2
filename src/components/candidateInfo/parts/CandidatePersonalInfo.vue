<template>
  <section class="personal-info">
    <h4 class="personal-info-title">Личная информация</h4>
    <section class="personal-info-table">

      <div class="personal-info-cell">
        <input-component v-model="lastName"
                         label="Фамилия"/>
      </div>

      <div class="personal-info-cell">
        <input-component v-model="firstName"
                         label="Имя"/>
      </div>

      <div class="personal-info-cell">
        <input-component v-model="middleName"
                         label="Отчество"/>
      </div>

      <div class="personal-info-cell">
        <input-component v-model="birthdayDate"
                         label="Дата Рождения"
                         type="date"/>
      </div>

      <div class="personal-info-cell">
        <select-component label="Гражданство"
                          id="citizenship"
                          :options="[{label: candidateCurrentState.citizenship, value: candidateCurrentState.citizenship},
                          {label: 'страна 2', value: 'страна 2'}, {label: 'страна 3', value: 'страна 3'}]"
                          :selected="candidateCurrentState.citizenship"
        @changeSelected="handleSelectedCitizenship">
        </select-component>
      </div>

      <div class="personal-info-cell">
        <radio-brn-group title="Пол"
                         :options="genderOptions"
        @newOptionsState="handleNewOptionsState"></radio-brn-group>
      </div>

      <div class="personal-info-cell">
        <input-component v-model="city"
                         label="Город"
                         is-large-width
                         is-disabled/>
      </div>

    </section>
  </section>
</template>

<script>
import InputComponent from "@/components/customizedComponents/InputComponent";
import SelectComponent from "@/components/customizedComponents/SelectComponent";
import RadioBrnGroup from "@/components/customizedComponents/RadioBtnGroup";

export default {
  name: "CandidatePersonalInfo",
  components: {
    RadioBrnGroup,
    SelectComponent,
    InputComponent
  },
  props: {
    candidate: {
      required: true
    }
  },
  computed: {
    candidateCurrentState() {
      return JSON.parse(JSON.stringify(this.candidate));
    },
    lastName: {
      get() {
        return this.candidateCurrentState.lastName
      },
      set(newLastName) {
        this.candidateCurrentState.lastName = newLastName;
        this.notifyAboutCandidateInfoChanges();
      }
    },
    firstName: {
      get() {
        return this.candidateCurrentState.firstName
      },
      set(newFirstName) {
        this.candidateCurrentState.firstName = newFirstName;
        this.notifyAboutCandidateInfoChanges();
      }
    },
    middleName: {
      get() {
        return this.candidateCurrentState.middleName
      },
      set(newLMiddleName) {
        this.candidateCurrentState.middleName = newLMiddleName;
        this.notifyAboutCandidateInfoChanges();
      }
    },
    birthdayDate: {
      get() {
        return this.candidateCurrentState.age
      },
      set(newDate) {
        this.candidateCurrentState.age = newDate;
        this.notifyAboutCandidateInfoChanges();
      }
    },
    city: {
      get() {
        return this.candidateCurrentState.city
      },
      set(newCity) {
        this.candidateCurrentState.city = newCity;
        this.notifyAboutCandidateInfoChanges();
      }
    },
    genderOptions() {
      return [
        {label: 'Женский', isChecked: this.isFemale(), name: 'gender', value: 'female'},
        {label: 'Мужской', isChecked: !this.isFemale(), name: 'gender', value: 'male'}]
    },
    update() {
      console.log("updated", this.candidateCurrentState)
      return this.candidateCurrentState;
    }
  },
  methods: {
    isFemale() {
      return this.candidateCurrentState.gender !== 'male';
    },
    notifyAboutCandidateInfoChanges() {
      this.$emit('newState', this.candidateCurrentState)
    },
    handleNewOptionsState() {
      this.$emit('changeGenderById', this.candidate.id )
    },
    handleSelectedCitizenship(newCitizenship){
      this.$emit('changeSelectedCitizenship', {id: this.candidate.id, citizenship: newCitizenship});
    }
  }
}
</script>

<style scoped>
.personal-info {
  padding: var(--offset-5xl) 0 var(--offset-xxl) 0;
  border-top: var(--offset-xxs) solid var(--border-color);
}

.personal-info-table {
  display: grid;
  grid-template-rows: repeat(3, 68px);
  grid-template-columns: repeat(3, 307px);
  gap: var(--offset-6xl);
  margin-top: var(--offset-6xl);
}

.personal-info-cell {
  display: flex;
  flex-direction: column;
  row-gap: var(--offset-m);
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

/*right side -> personal info block -> select*/
select {
  width: 100%;
  height: var(--offset-large);
  background: var(--background-input);
  border: var(--offset-xxs) solid transparent;
  border-radius: var(--offset-m);
  padding: 6px var(--offset-xxl);
  outline: none;
  appearance: none;
  background-image: url("../../../assets/arrow.svg");
  background-position: calc(100% - 18px) center;
  background-repeat: no-repeat;
  color: var(--input-value-color);
  box-sizing: border-box;
  font-weight: 400;
  font-size: var(--offset-4xl);
  line-height: var(--offset-5xl);
}

</style>