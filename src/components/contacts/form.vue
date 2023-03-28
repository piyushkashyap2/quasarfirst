<template>
  <div clas="column">
    <div>
      <h6 class="q-ma-none "> Contacts</h6>
    </div>
    <q-form class="q-my-md">
      <q-input dense label="ID" outlined v-model="formData.id" />
      <q-select class="q-my-xs" outlined v-model="formData.status" :options="options" label="Status" />
      <q-input class="q-my-xs" dense label="Sort" outlined v-model="formData.sort" />
      <q-input class="q-my-xs" dense label="Name" outlined v-model="formData.name" />
      <q-select class="q-my-sm" dense outlined :options="accountList" label="Account Id" v-model="formData.account_id"
        map-option option-label="account_name" option-value="id" emit-value use-input />

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

    }
  },
  watch: {
    accountSearchText(val) {
      this.fetchAccount()
    },
  },
  methods: {
    async submitData() {
      let response = await this.$api.post('/items/invoices', this.formData)
      console.log(response)
    },
    async fetchAccount() {
      let params = {}
      if (this.accountSearchText) {
        params.filter = { account_name: { _start_with: this.accountSearchText } }

      }
      let response = await this.$api.get('/items/accounts', { params })
      this.accountList = response.data.data

    },
  },
  created() {
    this.fetchAccount()
  }
}
</script>