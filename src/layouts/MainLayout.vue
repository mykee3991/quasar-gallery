<template>
  <q-layout view="lHh Lpr lFf">
    <q-header >
      <q-toolbar>
        <q-toolbar-title>
          Quasar Gallery Demo
        </q-toolbar-title>
        <q-space />
        <DarkToggle />
      </q-toolbar>
      <q-tabs
        v-model="tab"
        class="text-grey"
        :class="{'bg-grey-3': !$q.dark.isActive, 'bg-dark': $q.dark.isActive}"
        align="left"
      >
        <q-route-tab exact-active-class="text-primary" to="/" name="all" label="All" />
        <q-route-tab exact-active-class="text-primary" to="/nature" name="nature" label="Nature" />
        <q-route-tab exact-active-class="text-primary" to="/architecture" name="architecture" label="Architecture" />
      </q-tabs>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import EssentialLink from 'components/EssentialLink.vue'

const linksData = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  }
];

import { defineComponent, ref } from '@vue/composition-api';
import DarkToggle from "components/DarkToggle.vue"
export default defineComponent({
  name: 'MainLayout',
  components: { DarkToggle },
  setup() {
    const leftDrawerOpen = ref(false);
    const essentialLinks = ref(linksData);
    const tab = ref('all')

    return {leftDrawerOpen, essentialLinks,tab}
  }
});
</script>
