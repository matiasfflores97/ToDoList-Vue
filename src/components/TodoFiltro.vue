<template>
  <div class="card mt-3">
      <div class="card-body d-flex justify-content-between align-items-center">
          <span role="button" @click="filter('actives')">
              Actives
          </span>
          <span role="button" @click="filter('all')">
              All
          </span>
          <span role="button" @click="filter('completed')">
              Completed
          </span>
      </div>
  </div>
</template>

<script>
import { inject } from '@vue/runtime-core'
export default {

    setup(){
        const status = inject('status')

        const filter = state => {
            status.value = state
        }

        return { filter }
    }

}
</script>

<style>

</style>