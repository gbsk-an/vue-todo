<template>
<section class="width: 100%" style="background-color: #e2d5de;">
    <div class="container py-5 h-100">
        <div class="row d-flex justify-content-center align-items-center h-100">
            <div class="col col-xl-10">
                <div class="card" style="border-radius: 15px;">
                    <div class="card-body">
                      <div class="mb-5">
                        <h3 class="mb-4">Things todo today</h3>
                        <div class="d-flex flex-row justify-content-between card-body_top">
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
                          <input-default 
                            v-model="searchTasks"
                            placeholder="Search"
                          />
                          <select-default 
                            v-model="selectedSort"
                            :options="sortOptions"
                          />
                        </div>                        
                      </div>                                                
                      <ToDoList
                        :tasks="sortedAndsearchTasks"
                        @remove="removeTask"
                        v-if="!isTasksLoading"
                      />
                      <div v-else>
                        <p>Loading...</p>
                      </div>
                      <nav aria-label="...">
                        <ul class="pagination pagination-lg">
                          <li 
                            v-for="pageCurrent in totalPage" 
                            :key="page" 
                            class="page-item" 
                            aria-current="page">
                              <span 
                                class="page-link" 
                                :class="{
                                  'page-item active': page === pageCurrent
                                }"
                                @click="changePage(pageCurrent)"
                              >
                                {{pageCurrent}}
                            </span>
                          </li>
                        </ul>
                      </nav>
                    </div>                
                </div>
            </div>
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
        sortOptions: [
          {value: 'title', name: 'title'},
          {value: 'body', name: 'description'}
        ],
        page: 1,
        limit: 10,
        totalPage: 0,
        selectedSort: '',
        searchTasks: '',
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
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit
            }
          });
          this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit) 
          // this.tasks = response.data;
        } catch (e) {
          alert('Error')
        } finally {
          this.isTasksLoading = false;
        }
      },
      changePage(pageCurrent) {
        this.page = pageCurrent
        // this.fetchTasks()
      },
      showModal() {
        this.modalVisibility = true;
      }
    },
    mounted() {
      // this.fetchTasks();
    },
    computed: {
      sortedTasks() {
        return [...this.tasks].sort((a, b) => a[this.selectedSort]?.localeCompare(b[this.selectedSort]))
      },
      sortedAndsearchTasks() {
        return this.sortedTasks.filter(task => task.title.toLowerCase().includes(this.searchTasks.toLowerCase()))
      }
    },
    // watch: {
    //   selectedSort(newValue) {
    //     this.tasks.sort((a, b) => {
    //       return a[newValue]?.localeCompare(b[newValue])
    //     })
    //   },
    // }
  }
  </script>
  
<style lang="scss" scoped>
.card-body {
  padding: 3em;

  &_top {
    gap: 2em;
  }
}
</style>