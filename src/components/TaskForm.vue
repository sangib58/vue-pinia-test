<template>
    <form @submit.prevent="handleSubmit">
        <input 
            type="text"
            placeholder="I need to...."
            v-model="newTask"
        >
        <button>Add Task</button>
    </form>
</template>

<script>
import { ref } from 'vue';
import { useTaskStore } from '../../store/TaskStore';
    export default {
        setup(){
            const newTask=ref('')
            const taskStore=useTaskStore()
            const handleSubmit=()=>{
                if(newTask.value.length>1){
                        taskStore.addTask({
                        id:Math.floor(Math.random()*10000),
                        title:newTask.value,
                        isFav:false
                    })
                    newTask.value=''
                }
                
            }
            return{handleSubmit,newTask}
        }
   
    }
</script>