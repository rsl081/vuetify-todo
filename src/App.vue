<template>
  <v-app id="inspire">
    <v-navigation-drawer 
      v-model="drawer"
      app
    >
      <v-img
        class="pa-4 pt-7"
        src="https://picsum.photos/id/11/500/300"
        height="170"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
      >
        <v-avatar 
          class="mb-2"
          size="70"
        >
          <img
            src="./assets/portpic3.png"
            alt="Russel"
          >
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
          Russel Rodriguez
        </div>
        <div class="white--text text-subtitle-2">
          09616925025
        </div>
      </v-img>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
          <dialog-delete 
            v-if="dialogs.delete"
            @close="dialogs.delete = false"
            :task="task"
          />
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="primary"
      dark
      src="https://picsum.photos/1920/1080?random"
      prominent
      height="170"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        ></v-img>
      </template>

      <v-container class="pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon> 

          <v-spacer></v-spacer>

          <search />
        </v-row>
        <v-row>
          <v-toolbar-title class="text-h4 ml-4">Todo List</v-toolbar-title>
        </v-row>
        <v-row>
          <live-date-time />
        </v-row>
      </v-container>



    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
import Snackbar from './components/Shared/Snackbar.vue'
import LiveDateTime from './components/Tools/LiveDateTime.vue'
import Search from './components/Tools/Search.vue'
  export default {
  components: { Snackbar, Search, LiveDateTime },
    data: () => ({
      drawer: null,
      dialogs: {
        delete: false,
      },
      items: [
        { title: 'Dashboard',
          icon: 'mdi-format-list-checks', 
          to: '/'
        },
        { title: 'About',
          icon: 'mdi-help-box', 
          to: '/about',
        },
      ],
    }),

    mounted () {
      this.$store.dispatch('getTasks')
    }
  }
</script>
