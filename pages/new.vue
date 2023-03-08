<template>
    <div>
        <SASTaskPageHeader 
            title="New House Rule" 
            button-title="BACK" 
            variant="danger"
            @buttonClick="$router.back()" 
        />

        <SASTaskHouseRuleForm 
            v-bind:name.sync="house_rules.name"
            v-bind:active.sync="house_rules.active"
            @formSubmit="create"
        >
            <b-button type="submit" variant="primary">
                CREATE
            </b-button>
        </SASTaskHouseRuleForm>
    </div>
</template>

<script>
export default {
    layout: 'dashboard',
    data() {
        return {
            isFormModalOpen: false,
            house_rules: {
                name: null,
                active: null
            }
        }
    },
    methods: {
        async create() {
            await this.$axios.$post('/api/admin/house_rules', {
                house_rules: this.house_rules
            })

            this.$router.push('/')
        },
    }
}
</script>
