<template>
    <div v-cloak v-show="entity">
        <SASTaskPageHeader 
            title="New House Rule" 
            button-title="BACK" 
            variant="danger"
            @buttonClick="$router.back()" 
        />

        <SASTaskHouseRulesDetails :active="entity?.active" :order="entity?.order" />

        <b-row v-if="!isFormOpen">
            <b-button variant="primary" @click="isFormOpen = true">UPDATE</b-button>
            <b-button variant="danger" @click="isDeleteModalOpen = true">DELETE</b-button>
        </b-row>
        <SASTaskHouseRuleForm 
            v-else
            v-bind:name.sync="house_rules.name"
            v-bind:active.sync="house_rules.active"
            @formSubmit="create"
        >
            <b-button type="submit" variant="primary">
                UPDATE
            </b-button>

            <b-button variant="danger" @click="isFormOpen = false">
                CANCEL
            </b-button>
        </SASTaskHouseRuleForm>

        <b-modal 
            v-model="isDeleteModalOpen" 
            centered 
            :title="`Delete '${entity?.name}'?`"
            busy="true"
        >
            <p>You cannot undo this action.</p>
            <template #modal-footer="{ ok, cancel}">
                <b-button size="sm" variant="success" @click="isDeleteModalOpen = false">
                    CANCEL
                </b-button>
                
                <b-button size="sm" variant="danger" @click="remove">
                    DELETE
                </b-button>
            </template>
        </b-modal>
    </div>
</template>

<script>
export default {
    layout: "dashboard",
    data() {
        return {
            entity: null,
            isFormOpen: false,
            isDeleteModalOpen: false,
            house_rules: {
                name: null,
                active: null
            }
        }
    },
    async fetch() {
        const { id } = this.$route.params

        const { data } = await this.$axios.$get(`/api/admin/house_rules/${id}`)

        this.entity = data
    },
    methods: {
        async remove() {
            const { id } = this.$route.params
            await this.$axios.$delete(`api/admin/house_rules/${id}`)
            this.$router.push('/')
        },
        async update() {
            const { id } = this.$route.params
            await this.$axios.$put(`/api/admin/house_rules/${id}`, {
                house_rules: this.house_rules
            })
            this.isFormOpen = false
            this.$fetch()
        }
    }
}
</script>
