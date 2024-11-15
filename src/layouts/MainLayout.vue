<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated>
      <q-toolbar class="top">
        <q-btn flat icon="home" to="#top" aria-label="Home" />
        <q-space />
        <q-tabs v-model="tab" align="center">
          <q-tab name="home" label="HOME" to="#HOME" />
          <q-tab name="menu" label="MENU" to="#MENU" />
          <q-tab name="products" label="PRODUCTS" to="#PRODUCTS" />
          <q-tab name="about" label="ABOUT" to="#ABOUT" />
          <q-tab name="contact" label="CONTACT US" to="#CONTACT-US" />
        </q-tabs>
        <q-space />
        <q-btn flat icon="person" />
        <q-btn flat icon="shopping_basket" @click="showCart" />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer class="text-center">
      <div>تمامی حقوق این صفحه متعلق به بنده است ©</div>
      <q-list>
        
      </q-list>
    </q-footer>
  </q-layout>
</template>


<script setup>
import { ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";

defineOptions({
  name: "MainLayout",
});

const linksList = [
  {
    title: "Docs",
    caption: "quasar.dev",
    icon: "school",
    link: "https://quasar.dev",
  },
  {
    title: "Github",
    caption: "github.com/quasarframework",
    icon: "code",
    link: "https://github.com/quasarframework",
  },
  {
    title: "Discord Chat Channel",
    caption: "chat.quasar.dev",
    icon: "chat",
    link: "https://chat.quasar.dev",
  },
  {
    title: "Forum",
    caption: "forum.quasar.dev",
    icon: "record_voice_over",
    link: "https://forum.quasar.dev",
  },
  {
    title: "Twitter",
    caption: "@quasarframework",
    icon: "rss_feed",
    link: "https://twitter.quasar.dev",
  },
  {
    title: "Facebook",
    caption: "@QuasarFramework",
    icon: "public",
    link: "https://facebook.quasar.dev",
  },
  {
    title: "Quasar Awesome",
    caption: "Community Quasar projects",
    icon: "favorite",
    link: "https://awesome.quasar.dev",
  },
];

const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}
</script>


<style>
.top {
  display: flex;
  justify-content: space-between;
  height: 100px;
  background-color: black;
}
</style>
