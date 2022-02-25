<template>
  <form @submit.prevent="addTask">
      <input 
      class="form-control my-3"
      type="text"
      placeholder="Insert task"
      v-model.trim="currentTask">
  </form>
</template>

<script>
import { inject, ref } from 'vue'
export default {
    setup(){
        const ToDos = inject('ToDos')
        const currentTask = ref('')

        const addTask = () => {
            if(currentTask.value === ''){
                console.log('Empty')
                return
            }

            ToDos.value.push({
                id: Date.now(),
                task: currentTask.value,
                edit: false,
                completed: false
            })

            localStorage.setItem('ToDos', JSON.stringify(ToDos.value))

            currentTask.value = ''
        }

        return { addTask, currentTask }
    }
}
</script>

<style>

</style>