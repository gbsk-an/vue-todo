<template>
<div>
    <ul v-if="tasks.length > 0" class="list-group mb-0">
    <h4 class="mb-3">List</h4>
        <ToDoItem
            v-for="task in tasks" 
            :task="task" 
            :key="task.id"
            @remove="$emit('remove', task)"       
        />
    </ul>
    <h2 v-else>You have nothing to do</h2>
</div>

</template>

<script>
import ToDoItem from '@/components/todo-item.vue';
export default {
    name: "todo-list",
    components: {
        ToDoItem
    },
    props: {
        tasks: {
            type: Array,
            required: true
        }
    }
}
</script>

<style lang="scss" scoped>

</style>