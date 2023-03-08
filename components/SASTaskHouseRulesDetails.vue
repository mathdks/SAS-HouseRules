<template>
    <div>
        <b-row>
            <b-col>
                <p>Active: {{ active }}</p>
            </b-col>
        </b-row>

        <b-row>
            <b-col>
                <p>Order: {{ order }}</p>
            </b-col>
        </b-row>
    </div>
</template>

<script>
export default {
    props: {
        active: Number,
        order: Number
    }
}
</script>