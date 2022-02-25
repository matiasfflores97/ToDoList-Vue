<template>
    <div class="progress mb-3">
        <div 
        :class="['progress-bar', { 'bg-danger': todos <= 25, 'bg-warning': todos < 75, 'bg-success': todos >= 75 }]"
        :style="{ width: todos + '%' }" 
        role="progressbar" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100">
        {{todos}}%
        </div>
    </div>
</template>

<script>
import { computed, inject } from 'vue'
export default {
    setup(){
        const ToDos = inject('ToDos')

        const todos = computed(() => {
            const todosCompleted = ToDos.value.filter(item => item.completed === true).length
            return todosCompleted * 100 / ToDos.value.length
        })

        return { todos }
    }
}
</script>

<style>

</style>