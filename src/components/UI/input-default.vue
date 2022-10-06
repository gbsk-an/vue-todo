<template>
    <input 
        type="text" 
        id="form3" 
        class="form-control form-control-lg mb-4"
        :value="modelValue" 
        @input="updateInput"
    />
</template>

<script>
export default {
    name: 'input-default',
    props: {
        modelValue: [String, Number]
    },
    methods: {
        updateInput(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style lang="scss" scoped>
    
</style>