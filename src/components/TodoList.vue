<template>
    <ul class="list-group">
        <todo-progress 
            v-if="ToDos.length > 0"
        />
        <todo-item 
        v-for="todo of ToDos" :key="todo.id"
        :todo="todo"
        />
        <li v-if="ToDos.length === 0" class="list-group-item">Without ToDos...</li>
        <todo-footer
            v-if="ToDos.length > 0"
        />
        <todo-filtro 
            v-if="ToDos.length > 0"
        />
    </ul>
</template>

<script>
import { ref, inject, provide, computed } from 'vue'
import TodoItem from './TodoItem.vue'
import TodoFooter from './TodoFooter.vue'
import TodoFiltro from './TodoFiltro.vue'
import TodoProgress from './TodoProgress.vue'
export default {
  components: { TodoItem, TodoFooter, TodoFiltro, TodoProgress },
    setup(){
        const allToDos = inject('ToDos')
        const status = ref('all')

        const ToDos = computed(() => {
            if(status.value === 'all'){
                return allToDos.value
            }
            if(status.value === 'actives'){
                return allToDos.value.filter(item => item.completed === false)
            }
            if(status.value === 'completed'){
                return allToDos.value.filter(item => item.completed === true)
            }
        })

        provide('status', status)

        return { ToDos }
    }
}
</script>

<style>

</style>