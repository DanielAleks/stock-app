<template>
  <q-layout view="lHh Lpr lFf" class="main-bg-image">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title> Quasar App </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered class="bg-grey-1">
      <q-list>
        <q-item-label header class="text-grey-8">
          Essential Links
        </q-item-label>

        <EssentialLink
          v-for="to in essentialLinks"
          :key="to.title"
          v-bind="to"
          target="_blank"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<style lang="sass">
.main-bg-image
  background-image: url(../assets/stockBg.png)
@font-face
  font-family: "Oswald-B"
  src: url(../assets/fonts/static/Oswald-Bold.ttf)
@font-face
  font-family: "Nunito"
  src: url(../assets/fonts/Nunito-Regular.ttf)
// h3, p

// p
//   font-family: Nunito
//   font-size: 1.2rem
//   width: 20rem
//   margin-top: 2rem

h3
  width: 20rem
  font-family: oswald-b
  padding: 0px
  margin: 0px
  color: #fff
  margin-left: 5rem
</style>

<script lang="ts">
import EssentialLink from 'components/EssentialLink.vue';

const linksList = [
  {
    title: 'Post',
    caption: 'post your trades',
    icon: 'school',
    link: '#/post',
  },
  {
    title: 'Home',
    caption: 'home',
    icon: 'code',
    link: '#/',
  },
  {
    title: 'Review',
    caption: 'review your trades',
    icon: 'chat',
    link: '#/review',
  },
  {
    title: 'The App',
    caption: 'learn why I created this app and how it can help you.',
    icon: 'favorite',
    link: '/',
  },
];

import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink,
  },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
