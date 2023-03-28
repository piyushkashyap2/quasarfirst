<template>
  <div clas="column">
    <div>
      <h6 class="q-ma-none "> Account</h6>
    </div>
    <q-form class="q-my-md">
      <q-input dense lazy-rule :rules="nameRule" label="Account Name" outlined v-model="formData.account_name" />
      <q-input type="textarea" class="q-my-xs" dense label="Account Address" outlined
        v-model="formData.account_address" />
      <q-input class="q-my-xs" lazy-rule :rules="phoneRules" dense label="contact Number" outlined
        v-model="formData.account_number" />
      <q-input class="q-my-xs" dense label="Email" outlined v-model="formData.email" />
      <q-input :rules="[validationMandatory, validationNoSymbols]" class="q-my-xs" dense label="City" outlined
        v-model="formData.city" />
      <q-select outlined :options="['published', 'Draft', 'archived']" label="Status" v-model="formData.status" />
      <q-input class="q-my-xs" dense label="Pin Code" outlined v-model="formData.pin_code" />
      <q-input class="q-my-xs" dense label="Country" outlined v-model="formData.country" />

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
      formData: {}

    }
  },
  setup() {
    return {
      phoneRules: [
        val => (val && val.length == 10) || 'Phone number is not valid'
      ],
      nameRule: [
        val => !!val || 'Field is required'
      ]
    }
  },
  methods: {
    async submitData() {
      let response = await this.$api.post('/items/accounts', this.formData)
      console.log(response)
    }

  },
}
</script>
