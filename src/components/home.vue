<template>
<section class="width: 100%" style="background-color: #e2d5de;">
    <div class="container py-5 h-100">
        <div class="row d-flex justify-content-center align-items-center h-100">
            <div class="col col-xl-10">
                <div class="card" style="border-radius: 15px;">
                    <div class="card-body p-5">
                      <div class="mb-5">
                        <h3 class="mb-4">Things todo today</h3>
                        <button-default
                        @click="showModal"
                        >
                          Add task
                        </button-default>
                        <modal v-model:show="modalVisibility">
                            <ToDoForm
                              @create="addTask"
                            />
                        </modal>
                      </div>                                                
                      <ToDoList
                        :tasks="tasks"
                        @remove="removeTask"
                        v-if="!isTasksLoading"
                      />
                      <div v-else>
                        <p>Loading...</p>
                      </div>
                    </div>                
                </div>
            </div>
            <button @click="fetchTasks"></button>
        </div>
    </div>
</section>
<FooterDefault />
</template>
  
  <script>
  import ToDoForm from "@/components/TodoForm.vue"
  import ToDoList from "@/components/TodoList.vue"
  import FooterDefault from "@/components/FooterDefault.vue"

  import axios from "axios"

  export default {
    name: "home",
    components: {
      ToDoForm,
      ToDoList,
      FooterDefault
    },
    data() {
      return {
        tasks: [
          {id: 1, title: 'Visit local farmers market', body: 'Pick out some fresh produce'},
          {id: 2, title: 'Grab a coffee', body: 'Starbucks'},
        ],
        isTasksLoading: false,
        modalVisibility: false,
      }
    },
    methods: {
      addTask(task) {
        this.tasks.push(task);
        this.modalVisibility = false;
      },
      removeTask(task) {
        this.tasks = this.tasks.filter(t => t.id !== task.id)
      },
      async fetchTasks() {
        try {
          this.isTasksLoading = true
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
          this.tasks = response.data;
        } catch (e) {
          alert('Error')
        } finally {
          this.isTasksLoading = false;
        }
      },
      showModal() {
        this.modalVisibility = true;
      }
    },
    mounted() {
      this.fetchTasks();
    }
  }
  </script>
  
  <style lang="scss" scoped>

  </style>