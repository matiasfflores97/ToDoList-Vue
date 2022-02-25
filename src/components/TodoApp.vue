<template>
    <h1>ToDo</h1>
    <todo-form />
    <todo-list />
</template>

<script>
import { provide, ref, watchEffect } from 'vue'
import TodoForm from './TodoForm.vue'
import TodoList from './TodoList.vue'
export default {
    components: { TodoForm, TodoList },
    setup(){
        const ToDos = ref([])
        provide('ToDos', ToDos)

        if(localStorage.getItem('ToDos')){
            ToDos.value = JSON.parse(localStorage.getItem('ToDos'))
            ToDos.value = ToDos.value.map(item => {
                if(item.edit){
                    item.edit = false
                }

                return item
            })
        }

        watchEffect(() => {
            localStorage.setItem('ToDos', JSON.stringify(ToDos.value))
        })
    }
}
</script>