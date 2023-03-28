<template>
  <div clas="column">
    <div>
      <h6 class="q-ma-none ">Menu</h6>
    </div>
    <q-form class="q-my-md">
      <q-input dense label="ID" outlined v-model="formData.id" />
      <q-input class="q-my-xs" dense label="Name" outlined v-model="formData.name" />
      <q-input class="q-my-xs" dense label="Sequence" outlined v-model="formData.sequence" />
      <q-select outlined :options="['published', 'Draft', 'archived']" label="Status" v-model="formData.status" />

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
  methods: {
    async submitData() {
      let response = await this.$api.post('/items/menu', this.formData)
      console.log(response)
    }

  },
}
</script>
