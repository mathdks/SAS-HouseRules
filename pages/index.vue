<template>
    <div>
        <SASTaskPageHeader 
            title="House Rules" 
            button-title="NEW"
            variant="primary"
            @buttonClick="$router.push('/new')" 
        />

        <b-row>
            <b-col v-for="entity in entities" :key="entity.id" class="col-12 col-md-4">
                <SASTaskHouseRulesCard 
                    :name="entity.name"
                    :active="entity.active"
                    :order="entity.order"
                    @open="$router.push(`/${entity.id}`)"
                />
            </b-col>
        </b-row>

        <b-modal v-model="isHouseRuleModalOpen">
            {{ houseRuleData }}
        </b-modal>
    </div>
</template>

<script>

export default {
    layout: "dashboard",
    data() {
        return {
            entities: null,
            isHouseRuleModalOpen: false,
            houseRuleData: null,
            isFormModalOpen: false,
            house_rules: {
                name: null,
                active: null
            }
        };
    },
    async fetch() {
        const { data } = await this.$axios.$get("/api/admin/house_rules");
        this.entities = data.entities;
    },
}
</script>
