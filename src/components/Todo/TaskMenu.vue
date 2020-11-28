<template>
    <div>
        <v-menu
        bottom
        left
        >
            <template v-slot:activator="{ on, attrs }">
                <v-btn
                color="primary"
                icon
                v-bind="attrs"
                v-on="on"
                >
                <v-icon>mdi-dots-vertical</v-icon>
                </v-btn>
            </template>

            <v-list>
                <v-list-item
                v-for="(item, i) in items"
                :key="i"
                @click="handleClick(i)"
                >
                <v-list-item-icon>
                    <v-icon v-text="item.icon"></v-icon>
                </v-list-item-icon>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item>
            </v-list>
        </v-menu>
        <dialog-delete 
            v-if="dialogs.delete"
            @close="dialogs.delete = false"
            :task="task"
        />
        <dialog-due-date
            @close="dialogs.dueDate = false"
            v-if="dialogs.dueDate"
            :task="task"
        />
        <dialog-edit
            v-if="dialogs.edit"
            @close="dialogs.edit = false"
            :task="task"
        />
    </div>
</template>

<script>
import DialogDelete from './Dialogs/DialogDelete.vue'
import DialogDueDate from './Dialogs/DialogDueDate.vue'
import DialogEdit from './Dialogs/DialogEdit.vue'
export default {
    props: [ 'task' ],
    components: { DialogDelete, DialogEdit, DialogDueDate },
    data: () => ({
      dialogs: {
          edit: false,
          dueDate: false,
          delete: false
      },
      items: [
        { 
            title: 'Edit', 
            icon: 'mdi-pencil',
            click() {
                this.dialogs.edit = true
            }
        },
        { 
            title: 'Due Date',
            icon: 'mdi-calendar',
            click() {
                this.dialogs.dueDate = true
            }   
        },
        { 
            title: 'Delete', 
            icon: 'mdi-delete',
            click() {
                this.dialogs.delete = true
            }
        },
      ],
    }),

    methods: {
        handleClick(index){
            this.items[index].click.call(this)   
        }
    }
}
</script>

<style>

</style>