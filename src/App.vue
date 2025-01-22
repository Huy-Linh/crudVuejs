<template>
  <div class="container">
    <v-app>
      <v-layout>
        <v-app-bar
          :elevation="1"
          color="info">
          <v-app-bar-nav-icon
            @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-app-bar-title>Application Bar</v-app-bar-title>
          <v-spacer></v-spacer>
          <v-btn>
            <font-awesome-icon icon="fa-solid fa-lightbulb" />
          </v-btn>
        </v-app-bar>
        <v-navigation-drawer
          v-model="drawer"
        >
          <v-list density="compact" nav>
            <v-list-item
              prepend-icon="mdi-view-dashboard"
              title="Home"
              value="home"
            ></v-list-item>
            <v-list-item
              prepend-icon="mdi-forum"
              title="About"
              value="about"
            ></v-list-item>
          </v-list>
        </v-navigation-drawer>
        <v-main>
          <Test2></Test2>
        </v-main>
        <AppFooter/>
      </v-layout>
    </v-app>
  </div>

</template>
<script setup>
  import Test2 from './components/Test2.vue'
  import AppFooter from "@/components/AppFooter.vue";
  import  { ref } from "vue";
  const drawer = ref(false)
  const tabName = ref('Test2');

</script>
<style scoped>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

</style>
