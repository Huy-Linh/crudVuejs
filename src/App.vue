<template>
  <div class="container">
    <v-app>
      <v-layout>
        <v-navigation-drawer
          v-model="drawer"
        >
          <v-list density="compact" nav>
            <v-list-item
              prepend-icon="mdi-view-dashboard"
              title="Home"
              value="home"
              href="#/helloworld"
            ></v-list-item>
            <v-list-item
              prepend-icon="mdi-forum"
              title="Crud"
              value="crud"
              href="#/"
            ></v-list-item>
          </v-list>
        </v-navigation-drawer>
        <v-app-bar
          :elevation="1"
          color="info">
          <v-app-bar-nav-icon
            @click="drawer = !drawer"><v-icon icon="mdi-dots-vertical"></v-icon></v-app-bar-nav-icon>
          <v-app-bar-title>Application Bar</v-app-bar-title>
          <v-spacer></v-spacer>
        </v-app-bar>
        <v-main>
          <KeepAlive>
            <component :is="currentView"/>
          </KeepAlive>
<!--          <FormInput/>-->
        </v-main>
      </v-layout>
    </v-app>
  </div>

</template>
<script setup>
  //import Test2 from './components/Test2.vue'
  // import HelloWorld from './components/HelloWorld.vue'
  import FormInput from './components/FormInput.vue'
  import  { ref, computed } from "vue";
  import { defineAsyncComponent } from 'vue'
  const HelloWorld = defineAsyncComponent({
    loader: () => import('./components/HelloWorld.vue'),
    loading: { template: '<div>Loading...</div>' },
    error: { template: '<div>Error!</div>' },
    delay: 200,
    timeout: 3000
    }
  )
  const Test2 = defineAsyncComponent(() =>
  import('./components/Test2.vue')
  )
  const drawer = ref(false)
  const routes = {
    '/': Test2,
    '/helloworld': HelloWorld,
  }
  const currentPath = ref(window.location.hash)
  window.addEventListener("hashchange", () => {
    currentPath.value = window.location.hash
  })
  const currentView = computed(() => {
    return routes[currentPath.value.slice(1) || '/'] || NotFound
  })

</script>
<style scoped>

</style>
