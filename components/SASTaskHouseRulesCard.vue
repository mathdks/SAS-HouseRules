<template>
    <b-card class="mb-4 w-100" :title="name">
        <SASTaskHouseRulesDetails :active="active" :order="order" />

        <b-button variant="success" @click="$emit('open')">
            SHOW
        </b-button>
    </b-card>
</template>

<script>
export default {
    props: {
        name: {
            type: String,
            required: true
        },
        active: {
            type: Number,
            required: true
        },
        order: {
            type: Number,
            required: true
        }
    }
}
</script>