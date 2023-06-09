<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <v-app id="laplap" class="flex-sm-fill" style="position: unset;">
    <v-navigation-drawer v-model="drawer" class="flex-sm-fill">
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>LapLap</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <div class="flex-sm-fill">
        <RouterView />
      </div>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({ 
      drawer: null,
      items: [
        {
          icon: 'mdi-apps',
          title: 'data 1',
          to: '/'
        },
        {
          icon: 'mdi-apps',
          title: 'data 2',
          to: '/about'
        }
      ],
    }),
  }
</script> 
<style>

  #app {
    /* max-width: 1280px; */
    margin: 0 auto;
    padding: 0rem;
    font-weight: normal;
  }

  #laplap .v-application__wrap {
  backface-visibility: hidden;
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  max-width: 100%;
  min-height: 100vh;
  min-height: 100dvh;
  position: unset;
  }

</style>


