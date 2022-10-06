<template>
    <button 
        type="submit" 
        class="btn btn-primary btn-lg btn-default"
    >
    <slot>

    </slot>
    </button>
</template>

<script>
export default {
    name: 'button-default'
}
</script>

<style lang="scss" scoped>
.btn-default {
    width: fit-content;
}
</style>