<template>
    <v-dialog
      :value="true"
      persistent
      max-width="290"
    >
      <v-card>
        <v-card-title class="headline">
          Edit Task
        </v-card-title>
          <v-card-text>
            Edit the title of this task
            <v-text-field 
                v-model="taskTitle"
                @keyup.enter="saveTask()"
            />    
          </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            text
            @click="$emit('close')"
          >
            Cancel
          </v-btn>
          <v-btn
            @click="saveTask()"
            :disabled="tastTitleInvalid"
            color="red darken-1"
            text
          >
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>

<script>
export default {
    props: ['task'],
    data() {
        return {
            taskTitle: null,
        }
    },
    computed: {
        tastTitleInvalid() {
            return !this.taskTitle || this.taskTitle === this.task.title
        }
    },
    methods: {
        saveTask(){
            if(!this.tastTitleInvalid){
                let payload = {
                    id: this.task.id,
                    title: this.taskTitle
                }

                this.$store.dispatch('updateTask', payload)
                this.$emit('close')
            }
        }
    },
    mounted() {
        this.taskTitle = this.task.title
    }
}
</script>

<style>

</style>