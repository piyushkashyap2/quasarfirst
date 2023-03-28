<template>
  <div clas="column">
    <div>
      <h6 class="q-ma-none "> Banks</h6>
    </div>
    <q-form class="q-my-md">
      <q-input dense label="ID" outlined v-model="formData.id" />
      <q-input class="q-my-xs" dense label="sort" outlined v-model="formData.sort" />
      <q-input class="q-my-xs" dense label="Bank Name" outlined v-model="formData.bank_name" />
      <q-input class="q-my-xs" dense label="Account Name" outlined v-model="formData.account_name" />
      <q-input class="q-my-xs" dense label="Account Number" outlined v-model="formData.account_no" />
      <q-input class="q-my-xs" dense label="IFSC" outlined v-model="formData.ifsc" />
      <q-input class="q-my-xs" dense label="Branch" outlined v-model="formData.branch" />
      <q-select class="q-my-sm" @filter="(val, done) => { organisationSearchText = val; done() }" dense outlined
        :options="organisationList" label="Oranisation Id" v-model="formData.organisation_id" map-option
        option-label="organisation_name" option-value="id" emit-value use-input />

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
      organisationSearchText: '',
      organisationList: [],

    }
  },
  watch: {
    OrganisationSearchText(val) {
      this.fetchOraganisation()
    },
  },
  methods: {
    async submitData() {
      let response = await this.$api.post('/items/banks', this.formData)
      console.log(response)
    },
    async fetchOrganisation() {
      let params = {}
      if (this.organisationSearchText) {
        params.filter = { organisaton_name: { _start_with: this.organisationSearchText } }

      }
      let response = await this.$api.get('/items/organisation', { params })
      this.organisationList = response.data.data

    },

  },
  created() {
    this.fetchOrganisation()
  }
}
</script>
