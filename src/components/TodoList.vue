<template>
<div>
    <ul v-if="tasks.length > 0" class="list-group mb-0">
    <h4 class="mb-3">List</h4>
    <transition-group name="task-list">
        <ToDoItem
            v-for="task in tasks" 
            :task="task" 
            :key="task.id"
            @remove="$emit('remove', task)"       
        />
    </transition-group>        
    </ul>
    <h2 v-else>You have nothing to do</h2>
</div>

</template>

<script>
import ToDoItem from '@/components/TodoItem.vue';
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
.task-list-item {
    display: inline-block;
    margin-right: 10px;
}
.task-list-enter-active,
.task-list-leave-active {
  transition: all .4s ease;
}
.task-list-enter-from,
.task-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
.task-list-move {
    transition: transform .4s ease;
}
</style>