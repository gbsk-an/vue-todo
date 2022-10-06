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
                        <PostList
                        :tasks="tasks"
                        />    
                    </div> 
                </div>
            </div>
        </div>
    </div>
</section>
  </template>
  
  <script>
  import ToDoForm from "@/components/todo-form.vue";
  import PostList from "@/components/todo-list.vue";
  export default {
    name: "home",
    components: {
      ToDoForm, PostList
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
      }
    }
  }
  </script>
  
  <style lang="scss" scoped>

  </style>