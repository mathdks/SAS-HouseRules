<template>
    <b-row class="mb-4">
        <b-col class="col-12 col-md-11">
            <h2>{{ title }}</h2>
        </b-col>
        <b-col class="col-12 col-md-1">
            <b-button :variant="variant" @click="$emit('buttonClick')">
                {{ buttonTitle }}
            </b-button>
        </b-col>
    </b-row>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            required: true
        },
        buttonTitle: {
            type: String,
            required: true
        },
        variant: {
            type: String,
            required: true
        }
    }
}
</script>