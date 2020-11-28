<template>
  <div class="home">
    <add-field-task></add-field-task>
    <list-task  v-if="$store.state.tasks.length" />
    <no-tasks v-else />
  </div>
</template>

<script>

import AddFieldTask from '../components/Todo/AddFieldTask.vue'
import ListTask from '../components/Todo/ListTask.vue'
import NoTasks from '../components/Todo/NoTasks.vue'

export default {
  name: 'Home',
  components: {
    AddFieldTask,
    ListTask,
    NoTasks,
  },
}
</script>