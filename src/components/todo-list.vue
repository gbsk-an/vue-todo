<template>
<ul class="list-group mb-0">
    <ToDoItem
        v-for="task in tasks" 
        :task="task"        
    />
</ul>
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