<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="logo">
      <h1>{{ taskStore.name }}</h1>
    </header>
    <!--Add New Task-->
    <TaskForm/>

    <!--Loading-->
    <div class="loading" v-if="loading">Loading....</div>

    <!-- Filter Task -->
    <nav class="filter">
      <button @click="filter='all'">All Tasks</button>
      <button @click="filter='favs'">Favourite Tasks</button>
    </nav>

    <!-- task list -->

    <div class="task-list" v-if="filter=='all'">
      <p>you have {{ totalCount }} tasks to do</p>
      <div v-for="task in tasks" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>

     <!-- Favourite task list -->
    <div class="task-list" v-if="filter=='favs'">
      <p>Favourite tasks {{ taskStore.favCount }}</p>
      <div v-for="task in taskStore.favs" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>

    <button @click="taskStore.$reset">Reset State</button>
  </main>
</template>

<script>
import { storeToRefs } from 'pinia';
import { useTaskStore } from '../store/TaskStore';
import TaskDetails from './components/TaskDetails.vue';
import TaskForm from './components/TaskForm.vue';
import { ref } from 'vue';

  export default {
    components:{TaskDetails, TaskForm},
    setup(){
      const taskStore=useTaskStore()
      //fetch tasks
      taskStore.getTasks()

      const {tasks,loading,favs,favCount,totalCount}=storeToRefs(taskStore)

      const filter=ref('all')

      return {taskStore,filter,tasks,loading,favs,favCount,totalCount}
    }
  }
</script>

<style scoped>

</style>