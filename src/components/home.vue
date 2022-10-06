<template>
<section class="vh-100" style="background-color: #e2d5de;">
    <div class="container py-5 h-100">
        <div class="row d-flex justify-content-center align-items-center h-100">
            <div class="col col-xl-10">    
                <div class="card" style="border-radius: 15px;">
                    <div class="card-body p-5">    
                        <h3 class="mb-3">Things todo today</h3>    
                        <ToDoForm
                        @create="addTask"
                        />
                        <ToDoList
                        :tasks="tasks"
                        @remove="removeTask"
                        />    
                    </div> 
                </div>
            </div>
        </div>
    </div>
</section>
<DefFooter />
</template>
  
  <script>
  import ToDoForm from "@/components/todo-form.vue";
  import ToDoList from "@/components/todo-list.vue";
  import DefFooter from "@/components/def-footer.vue"
  export default {
    name: "home",
    components: {
      ToDoForm, ToDoList, DefFooter
    },
    data() {
      return {
        tasks: [
          {id: 1, title: 'Visit local farmers market', body: 'Pick out some fresh produce'},
          {id: 2, title: 'Grab a coffee', body: 'Starbucks'},          
        ],
      }
    },
    methods: {
      addTask(task) {
        this.tasks.push(task);
      },
      removeTask(task) {
        this.tasks = this.tasks.filter(t => t.id !== task.id)
      }
    }
  }
  </script>
  
  <style lang="scss" scoped>

  </style>