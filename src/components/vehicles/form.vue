<template>
  <div clas="column">
    <div>
      <h6 class="q-ma-none "> vehicles</h6>
    </div>
    <q-form class="q-my-md">
      <q-input dense label="ID" outlined v-model="formData.id" />
      <q-select class="q-my-xs" outlined v-model="formData.status" :options="options" label="Status" />
      <q-input class="q-my-xs" dense label="Vehicle No" outlined v-model="formData.vehicle_no" />
      <q-select class="q-my-sm" @filter="(val, done) => { vehicleSearchText = val; done() }" dense outlined
        :options="vehicleList" label="Vehicle Type" v-model="formData.vehicle_type" map-option option-label="vehicle_no"
        option-value="id" emit-value use-input />
      <q-input class="q-my-xs" dense label="Fuel AVG" outlined v-model="formData.fuel_avg" />

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
      vehicleSearchText: '',
      vehicleList: [],

    }
  },
  watch: {
    vehicleSearchText(val) {
      this.fetchVehicle()
    }
  },
  methods: {
    async submitData() {
      let response = await this.$api.post('/items/vehicle', this.formData)
      console.log(response)
    },
    async fetchVehicle() {
      let params = {}
      if (this.vehicleSearchText) {
        params.filter = { vehicle_no: { _starts_with: this.vehicleSearchText } }

      }
      let response = await this.$api.get('/items/vehicles', { params })
      this.vehicleList = response.data.data

    },

  },
  created() {
    this.fetchVehicle()
  }
}
</script>
