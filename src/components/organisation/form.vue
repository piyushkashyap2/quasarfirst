<template>
    <div clas="column">
        <div>
            <h6 class="q-ma-none "> Organisation</h6>
        </div>
        <q-form class="q-my-md">
            <q-input type="textarea" class="q-my-xs" dense label="Address" outlined v-model="formData.address" />
            <q-input class="q-my-xs" dense label="City" outlined v-model="formData.city" />
            <q-input class="q-my-xs" dense label="Contact Number" outlined v-model="formData.contact_number" />
            <q-input class="q-my-xs" dense label="Country" outlined v-model="formData.country" />
            <q-input class="q-my-xs" dense label="Email" outlined v-model="formData.email" />
            <q-input class="q-my-xs" dense label="GST Number" outlined v-model="formData.gst_number" />
            <q-input class="q-my-xs" dense label="ID" outlined v-model="formData.id" />
            <q-input class="q-my-xs" dense label="Organisation Name" outlined v-model="formData.organisaation_name" />
            <q-select class="q-my-xs" outlined :options="['publised', 'Draft', 'archived']" label="status"
                v-model="formData.status" />


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
            let response = await this.$api.post('/items/organisation', this.formData)
            console.log(response)
        }

    },
}
</script>
  