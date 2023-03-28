<template>
    <div clas="column">
        <div>
            <h6 class="q-ma-none "> Invoices</h6>
        </div>
        <q-form class="q-my-md">
            <q-input class="q-my-sm" dense label="Grand Total" outlined v-model="formData.grand_total" />
            <q-input class="q-my-sm" dense label="ID" outlined v-model="formData.id" />
            <q-input dense class="q-my-sm" type="date" label="Invoice Date " stack-label outlined
                v-model="formData.invoice_date" />
            <q-input class="q-my-sm" dense label="Invoice Number" outlined v-model="formData.invoice_number" />
            <q-select dense outlined :options="['draft', 'provisional', 'final', 'cancelled']" label="Invoice Status"
                v-model="formData.invoice_status" />
            <q-select class="q-my-sm" dense outlined :options="['paid', 'parcially Paid', 'undaid']" label="Payment Status"
                v-model="formData.payment_status" />
            <q-select class="q-my-sm" @filter="(val, done) => { accountSearchText = val; done() }" dense outlined
                :options="accountList" label="Account Id" v-model="formData.account_id" map-option
                option-label="account_name" option-value="id" emit-value use-input />
            <q-select class="q-my-sm" @filter="(val, done) => { organisationSearchText = val; done() }" dense outlined
                :options="organisationList" label="Organisation Id" v-model="formData.organisation_id" map-option
                option-label="organisation_name" option-value="id" emit-value use-input />
            <q-input class="q-my-sm" dense label="Period" outlined v-model="formData.period" />
            <q-select class="q-my-sm" @filter="(val, done) => { bankSearchText = val; done() }" dense outlined
                :options="bankList" label="Bank Id" v-model="formData.bank_id" map-option option-label="bank_name"
                option-value="id" emit-value use-input />



        </q-form>
        <q-separator class=" q-my-md"></q-separator>
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
            organisationSearchText: '',
            organisationList: [],
            bankSearchText: '',
            bankList: []


        }
    },
    watch: {
        accountSearchText(val) {
            this.fetchAccount()
        },
        organisationSearchText(val) {
            this.fetchOraganisation()
        },
        bankSearchText(val) {
            this.fetchBank()
        }
    },
    methods: {
        async submitData() {
            let response = await this.$api.post('/items/invoices', this.formData)
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
        async fetchOrganisation() {
            let params = {}
            if (this.organisationSearchText) {
                params.filter = { organisation_name: { _starts_with: this.organisationSearchText } }

            }
            let response = await this.$api.get('/items/organisation', { params })
            this.organisationList = response.data.data

        },
        async fetchBank() {
            let params = {}
            if (this.bankSearchText) {
                params.filter = { bank_name: { _starts_with: this.bankSearchText } }

            }
            let response = await this.$api.get('/items/banks', { params })
            this.bankList = response.data.data

        },
    },
    created() {
        this.fetchAccount()
        this.fetchOrganisation()
        this.fetchBank()
    }
}
</script>
  