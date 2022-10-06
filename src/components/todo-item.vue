<template>
<li class="list-group-item d-flex justify-content-between align-items-center border-start-0 border-top-0 border-end-0 border-bottom rounded-0 mb-2">
    <div class="d-flex align-items-center gap-3">
        <input class="form-check-input" type="checkbox" value="" aria-label="..." />
        <div>
            <div class="d-flex flex-column">
                <h6>{{task.title}}</h6>
                <p>{{task.body}}</p>
            </div>
        </div>
    </div>
    <button-default>Delete</button-default>
</li> 
</template>

<script>    

export default {
    props: {
        task: {
            type: Object, 
            required: true
        }
    }
}
</script>

<style lang="scss" scoped>

</style>