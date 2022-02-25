<template>
    <li class="d-flex justify-content-between list-group-item">
        <span role="button">
            {{ activedToDos }} activos
        </span>
        <span role="button" @click="deleteCompleted">
            Delete completed
        </span>
    </li>
</template>

<script>
import { inject, computed } from 'vue'
export default {
    setup(){
        const ToDos = inject('ToDos')

        const activedToDos = computed(() => {
            return ToDos.value.filter(item => item.completed === false).length
        })

        const deleteCompleted = () => {
            ToDos.value = ToDos.value.filter(item => item.completed === false)
        }

        return { activedToDos, deleteCompleted }
    }
}
</script>

<style>

</style>