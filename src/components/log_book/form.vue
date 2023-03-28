<template>
  <div clas="column">
    <div>
      <h6 class="q-ma-none "> Log Book</h6>
    </div>
    <q-form class="q-my-md">
      <q-input class="q-my-xs" dense label="ID" outlined v-model="formData.id" />
      <q-select dense outlined :options="['published', 'Draft', 'archived']" label="Status" v-model="formData.status" />
      <q-input class="q-my-xs" dense label="Sort" outlined v-model="formData.sort" />
      <q-input class="q-my-xs" type="date" dense label="Date From" stack-label outlined v-model="formData.date_from" />
      <q-input class="q-my-xs" type="date" dense label="Date To" stack-label outlined v-model="formData.date_to" />
      <q-input class="q-my-xs" dense label="Initial reading" outlined v-model="formData.initial_reading" />
      <q-input class="q-my-xs" dense label="Final reading" outlined v-model="formData.Final_reading" />
      <q-select dense outlined :options="['Monthly', 'On Call']" label="Log Type" v-model="formData.log_type" />
      <q-select class="q-my-sm" @filter="(val, done) => { accountSearchText = val; done() }" dense outlined
        :options="accountList" label="Account Id" v-model="formData.account_id" map-option option-label="account_name"
        option-value="id" emit-value use-input />
      <q-select class="q-my-sm" @filter="(val, done) => { contactSearchText = val; done() }" dense outlined
        :options="contactList" label="Contact Id" v-model="formData.account_id" map-option option-label="name"
        option-value="id" emit-value use-input />
      <q-select class="q-my-sm" @filter="(val, done) => { vehicleSearchText = val; done() }" dense outlined
        :options="vehicleList" label="vehicle Id" v-model="formData.vehicle_id" map-option option-label="vehicle_no"
        option-value="id" emit-value use-input />
      <q-select class="q-my-sm" @filter="(val, done) => { driverSearchText = val; done() }" dense outlined
        :options="driverList" label="Driver Id" v-model="formData.driver_id" map-option option-label="driver_name"
        option-value="id" emit-value use-input />




    </q-form>
    <q-separator class="q-my-md"></q-separator>
    <div class="row q-my-md q-gutter-sm">
      <div>
        <q-btn label="Submit" color="green" unelevated @click="submitData"></q-btn>
      </div>
      <div>
        <q-btn label="Cancel" color="red" unelevated></q-btn>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      formData: {},
      accountSearchText: '',
      accountList: [],
      contactSearchText: '',
      contactList: [],
      vehicleSearchText: '',
      vehicleList: [],
      driverSearchText: '',
      driverList: [],

    }
  },
  watch: {
    accountSearchText(val) {
      this.fetchAccount()
    },
    contactSearchText(val) {
      this.fetchContact()
    },
    vehicleSearchText(val) {
      this.fetchVehicle()
    },
    driverSearchText(vaL) {
      this.fetchDriver()
    },
  },
  methods: {
    async submitData() {
      let response = await this.$api.post('/items/log_book', this.formData)
      console.log(response)
    },
    async fetchAccount() {
      let params = {}
      if (this.accountSearchText) {
        params.filter = { account_name: { _starts_with: this.accountSearchText } }

      }
      let response = await this.$api.get('/items/accounts', { params })
      this.accountList = response.data.data

    },
    async fetchContact() {
      let params = {}
      if (this.contactSearchText) {
        params.filter = { contact_name: { _starts_with: this.contactSearchText } }

      }
      let response = await this.$api.get('/items/contacts', { params })
      this.contactList = response.data.data

    },
    async fetchVehicle() {
      let params = {}
      if (this.vehicleSearchText) {
        params.filter = { vehicle_no: { _starts_with: this.vehicleSearchText } }

      }
      let response = await this.$api.get('/items/vehicles', { params })
      this.vehicleList = response.data.data

    },
    async fetchDriver() {
      let params = {}
      if (this.driverSearchText) {
        params.filter = { driver_name: { _starts_with: this.driverSearchText } }

      }
      let response = await this.$api.get('/items/driver', { params })
      this.driverList = response.data.data

    },

  },
  created() {
    this.fetchAccount()
    this.fetchContact()
    this.fetchVehicle()
    this.fetchDriver()
  }
}
</script>
