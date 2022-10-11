<template>
<form @submit.prevent class="d-flex flex-column flex-gap bd-highlight justify-content-center">
  <div class="form-outline d-flex flex-column flex-gap">
    <input-default
      v-model="task.title"
      type="text" 
      placeholder="task"
    />
    <input-default 
      v-model="task.body" 
      type="text" 
      placeholder="info"
    />
  </div>
  <button-default     
    @click="createTask"
  >
    Add
  </button-default>
</form>
</template>

<script>

export default {
  name: "todo-form",
    data() {
        return {
            task: {
                title: '',
                body: ''
            }
        }
    },
    methods: {
        createTask() {
          if (this.task.title.length != 0 && this.task.body.length != 0) {
            this.task.id = Date.now();
            this.$emit('create', this.task)
            this.task= {
                title: '',
                body: ''
            }
          } else {
            alert('you should write something')
          }            
        }
    },
}
</script>

<style lang="scss" scoped>
.flex-gap {
  gap: 1em;
}
</style>