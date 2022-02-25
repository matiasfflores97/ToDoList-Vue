<template>
    <li class="d-flex justify-content-between list-group-item">
        <input type="text" v-if="todo.edit" v-model="todo.task">
        <span role="button" v-else @click="completeTask(todo.id)" :class="{'text-line-through': todo.completed }">
            {{ todo.task }}
        </span>
        <div class="d-flex">
            <span class="mx-1" role="button" @click="modifyTask(todo.id)">
                <i v-if="todo.edit" class="fa-solid fa-check"></i>
                <i v-else class="fa-solid fa-pen-to-square"></i>
            </span>
            <span class="mx-1" role="button" @click="deleteTask(todo.id)">
                <i class="fa-solid fa-xmark"></i>
            </span>
        </div>
    </li>
</template>

<script>
import { inject } from 'vue'
export default {
    props: {
        todo: {
            type: Object,
            required: true
        }
    },
    setup(){
        const ToDos = inject('ToDos')

        const completeTask = id => {
            ToDos.value = ToDos.value.map(item => {
                if(item.id === id && item.completed === true){
                    item.completed = false
                    return item
                }
                if(item.id === id){
                    item.completed = true
                }

                return item
            })
        }

        const modifyTask = id => {
            ToDos.value = ToDos.value.map(item => {
                if(item.id === id){
                    item.edit ? item.edit = false : item.edit = true
                }

                return item
            })
        }

        const deleteTask = id => {
            ToDos.value = ToDos.value.filter(item => item.id !== id)
        }


        return { completeTask, modifyTask, deleteTask }
    }
}
</script>

<style>
.text-line-through{
    text-decoration: line-through;
}
</style>