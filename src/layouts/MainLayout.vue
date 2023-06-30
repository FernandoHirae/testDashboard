<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />

        <q-toolbar-title>
          Dashboard
        </q-toolbar-title>

        <q-btn round :icon="$q.dark.isActive ? 'dark_mode' : 'light_mode'" @click="$q.dark.toggle()" />

      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" :mini="miniState" @mouseover="miniState = false" @mouseout="miniState = true"
      :width="200" :breakpoint="500" show-if-above bordered>
      <q-list>
        <EssentialLink v-for="link in essentialLinks" :key="link.title" v-bind="link" />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Docs',
    caption: 'Dashboard Side Bar',
    icon: 'school',
    link: '/'
  },
  {
    title: 'Github',
    caption: 'Dashboard Side Bar',
    icon: 'code',
    link: '/'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'Dashboard Side Bar',
    icon: 'chat',
    link: '/'
  },
  {
    title: 'Forum',
    caption: 'Dashboard Side Bar',
    icon: 'record_voice_over',
    link: '/'
  },
  {
    title: 'Twitter',
    caption: 'Dashboard Side Bar',
    icon: 'rss_feed',
    link: '/'
  },
  {
    title: 'Facebook',
    caption: 'Dashboard Side Bar',
    icon: 'public',
    link: '/'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Dashboard Side Bar',
    icon: 'favorite',
    link: '/'
  }
]
const leftDrawerOpen = ref(false)

const miniState = ref(true)
const essentialLinks = linksList
function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

</script>
