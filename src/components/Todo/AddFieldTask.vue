<template>
    <v-text-field
    v-model="newTaskTitle"
    @keyup.enter="addTask"
    class="pa-3"
    outlined
    label="Add Task"
    hide-details
    clearable
    >
      <template v-slot:append>
        <v-icon
          @click="addTask"
          :disabled="tastTitleInvalid"
          color="primary"
        >
          mdi-plus
        </v-icon>
      </template>
    </v-text-field>
</template>

<script>
export default {
    data () { 
        return {
            newTaskTitle: '',
        }
    },
    computed: {
      tastTitleInvalid() {
          return !this.newTaskTitle
      }
    },
    methods: {
    addTask() {
      if(!this.tastTitleInvalid){
        this.$store.dispatch('addTask', this.newTaskTitle)
        this.newTaskTitle = ''
      }
    },
  }
}
</script>

<style>

</style>