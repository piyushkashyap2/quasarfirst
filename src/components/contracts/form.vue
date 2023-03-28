<template>
    <div clas="column">
        <div>
            <h6 class="q-ma-none "> Contracts</h6>
        </div>
        <q-form class="q-my-md">
            <q-input dense label="ID" outlined v-model="formData.id" />
            <q-input class="q-my-xs" dense label="Account" outlined v-model="formData.account" />
            <q-input class="q-my-xs" dense label="Vechile Type" outlined v-model="formData.vechile_type" />
            <q-input class="q-my-xs" dense label="Rent per month" outlined v-model="formData.rent_per_month" />
            <q-select class="q-my-xs" outlined v-model="formData.status" :options="['a', 'b']" label="fuel" />
            <q-input class="q-my-xs" dense label="Name" outlined v-model="formData.name" />
            <q-toggle label="Is Tax Included" v-model="formData.is_tax_included" />

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
            let response = await this.$api.post('/items/contracts', this.formData)
            console.log(response)
        }

    },
}
</script>
  