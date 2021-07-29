<template>
  <div id="app">
    <div class="container">
      <h1>Test Bootstrap</h1>
      <b-button v-b-modal.modal-newbemor>Yangi bemor</b-button>
      <b-table striped hover :items='patients'></b-table>
      <b-modal id="modal-newbemor" hide-footer title="Yangi bemor">
        <b-form-input v-model="patients.name" class="mb-3" placeholder="Ismingizni yozing"></b-form-input>
        <label for="example-datepicker">Tu'gilgan sana</label>
        <b-form-datepicker id="example-datepicker" v-model="patient.bdate" class="mb-3"></b-form-datepicker>
        <b-form-group label="Jinsni tanglang" v-slot="{ ariaDescribedby }">
          <div class="d-flex">
            <div class="mr-3">
              <b-form-radio v-model="patient.gender" :aria-describedby="ariaDescribedby" name="gender" class="mr-3"
                value="Erkak">Erkak</b-form-radio>
            </div>
            <div class="mr-3">
              <b-form-radio v-model="patient.gender" :aria-describedby="ariaDescribedby" name="gender" class="ml-3"
                value="Ayol">Ayol</b-form-radio>
            </div>
          </div>
        </b-form-group>
        <label for="doctor" class="mt-3">Shifokorni tanlang</label>
        <b-form-select v-model="patient.doctor" id="doctor" class="mp-3 form-control" :options="doctors">
        </b-form-select>
        <label for="time">Qabul vaqtini tanlang</label>
        <b-form-timepicker id="time" v-model="patient.time" locale="ru"></b-form-timepicker>
        <b-button variant="success" class="mt-3" @click="add()">Qo'shish</b-button>
      </b-modal>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'App',
    data() {
      return {
        patient: {},
        doctors: ['Bahodirov Aziz', 'Yo`ldoshev Farhod', 'Olimova Aziza'],
        patients: []
      }
    },
    methods: {
      add() {
        this.patients.push(this.patient)
        this.patient = {}
        localStorage.setItem('patients', JSON.stringify(this.patients))
        this.$bvModal.hide('modal-newbemor')
      }
    },
    created() {
      if (localStorage.getItem('patients')) {
        try {
          this.patients = JSON.parse(localStorage.getItem('patients'))
        } catch (error) {
          localStorage.removeItem('patients')
        }
      }
    }
  }
</script>

<style>
  .custom-radio {
    margin-right: 10px;
  }
</style>