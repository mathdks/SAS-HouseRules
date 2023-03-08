<template>
    <b-card>
        <b-form @submit.prevent="$emit('formSubmit')">
            <b-form-group id="input-group-1" label="Name:" label-for="input-name">
                <input 
                    id="input-name" 
                    class="form-control"
                    type="text" 
                    placeholder="Enter new name" 
                    required 
                    :value="name" 
                    @input="$emit('update:name', $event.target.value)" 
                />
            </b-form-group>
    
            <b-form-group id="input-group-2" label="Active:" label-for="input-active">
                <input 
                    id="input-active" 
                    class="form-control"
                    type="number" 
                    placeholder="Active" 
                    required 
                    :value="active" 
                    @input="$emit('update:active', $event.target.value)" 
                />
            </b-form-group>
    
            <slot />
        </b-form>
    </b-card>
</template>

<script>
export default {
    props: {
        name: String,
        active: Number
    },
    emits: ['update:name', 'update:active']
}
</script>
