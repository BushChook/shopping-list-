<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="no-print">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          Downer Forms
        </q-toolbar-title>

        <div>
          <q-btn flat label="Print" icon="print" @click="printForm" />
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item>
          <q-item-section>
            <q-select outlined v-model="model" :options="['Some Address 1', 'Some Address 2', 'Some Address 3']" label="Pick Job" />
          </q-item-section>
        </q-item>

        <q-item clickable tag="a" to="/pre-start-form">
          <q-item-section avatar>
            <q-icon name="list" />
          </q-item-section>

          <q-item-section>
            <q-item-label>Pre-Start Form</q-item-label>
            <q-item-label caption>The Pre-Start Form</q-item-label>
          </q-item-section>
        </q-item>

        <q-item clickable tag="a" to="/traffic-form">
          <q-item-section avatar>
            <q-icon name="list" />
          </q-item-section>

          <q-item-section>
            <q-item-label>Traffic Form</q-item-label>
            <q-item-label caption>The Traffic Form</q-item-label>
          </q-item-section>
        </q-item>

        <q-item clickable tag="a" to="/plant-checklist-form">
          <q-item-section avatar>
            <q-icon name="list" />
          </q-item-section>

          <q-item-section>
            <q-item-label>Plant Checklist Form</q-item-label>
            <q-item-label caption>Plant Checklist Form</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  },

  methods: {
    printForm() {
      this.leftDrawerOpen = false

      setTimeout(() => window.print(), 2000)
    }
  }
})
</script>
