<template>
  <div clas="column">
    <div>
      <h6 class="q-ma-none ">Items</h6>
    </div>
    <q-form class="q-my-md">
      <q-input dense label="ID" outlined v-model="formData.id" />
      <q-input class="q-my-xs" dense label="Item Name" outlined v-model="formData.item_name" />
      <q-select outlined :options="['service', 'service with rate']" label="Item Type" v-model="formData.item_type" />
      <q-select class="q-my-xs" outlined :options="['publised', 'Draft','archived']" label="status"  v-model="formData.status" />
      

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
      let response = await this.$api.post('/items/items', this.formData)
      console.log(response)
    }

  },
}
</script>
