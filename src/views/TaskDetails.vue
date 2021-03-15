<template>
    <div v-if="task" class="task-details">
        <h1>{{task.title}}</h1>
        <p>On {{task.date}} in {{task.location}} @ {{task.time}}</p>
        <button type="button" class="btn btn-secondary" @click="$router.go(-1)">Back</button>
    </div>
</template>

<script>
import TasksService from '@/services/TasksService.js'
export default {
  props: ['id'],
  data () {
    return {
      task: null
    }
  },

  created () {
    TasksService.getTask(this.id)
      .then(response => {
        console.log('task: ', response.data)
        this.task = response.data
      })
      .catch(error => {
        console.log('ERRORS' + error)
      })
  }
}
</script>

<style scoped>
.task-details{
    border:1px solid rgb(46, 141, 120);
    width:40%;
    margin:15px auto;
    padding:10px;
}
</style>
