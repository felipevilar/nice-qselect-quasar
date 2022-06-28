<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-icon name="checklist" size="md" />
        <q-toolbar-title>Reusable QSelect</q-toolbar-title>
      </q-toolbar>
    </q-header>
    <q-page-container>
      <router-view />
    </q-page-container>
    <q-footer>
      <q-toolbar class="text-center">
        <span class="full-width">
          Made by
          <a href="https://github.com/felipevilar" class="text-white text-bold">
            Felipe Vilar
          </a>
        </span>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'MainLayout',
});
</script>
