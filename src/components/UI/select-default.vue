<template>
    <select 
        v-model="modelValue" 
        class="form-select" 
        aria-label="Default select"
        @change="changeOption"
    >
        <option disable value="">Choose option</option>
        <option 
            v-for="option in options" 
            :key="option.value" 
            :value="option.value">
                {{option.name}}
        </option>
    </select>
</template>

<script>
export default {
    name: 'select-default',
    props: {
        modelValue: {
            type: String
        },
        options: {
            type: Array,
            default: () => []
        }
    },
    methods: {
        changeOption(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style lang="scss" scoped>
.form-select {
    width: fit-content;
}
</style>