<template>
  <tool-bar />
  <v-container>
    <v-row>
      <v-col cols="6">
        <h2 v-if="!isFetching">{{ filtered.length }} Contact(s)</h2>
      </v-col>
      <v-col cols="6">
        <v-text-field
          label="Search ..."
          variant="outlined"
          v-model="search"
        ></v-text-field>
      </v-col>
      <v-col cols="3" v-for="contact in filtered" :key="contact.id">
        <Card v-if="!isFetching" :contact="contact" />
      </v-col>
    </v-row>
    <div class="loader" v-if="isFetching"></div>
  </v-container>
</template>

<script lang="ts">
import { defineComponent, watch } from 'vue'
import { useContacts } from '../api/useContact'

// Components
import ToolBar from '../components/ToolBar.vue'
import Card from '../components/Card.vue'

export default defineComponent({
  name: 'HomeView',

  components: {
    ToolBar,
    Card,
  },
  setup() {
    const { isFetching, search, filtered, error, contacts } = useContacts()
    console.log(filtered)
    watch(search, useContacts)
    return { isFetching, search, filtered, error, contacts }
  },
})
</script>
<style>
.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #3498db; /* Blue */
  border-radius: 50%;
  width: 240px;
  height: 240px;
  animation: spin 2s linear infinite;
  margin: auto;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
