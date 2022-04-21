<template>
  <tool-bar />
  <v-container>
    <v-btn variant="plain" to="/">Home</v-btn>
    <v-card class="mx-auto" width="800">
      <v-img :src="contact.avatar" height="400px"></v-img>
      <v-card-title>
        {{ contact.first_name }} {{ contact.last_name }}
      </v-card-title>
      <v-card-subtitle>
        <v-icon large> mdi-email </v-icon>
        <p>{{ contact.email }}</p>
      </v-card-subtitle>
      <v-card-subtitle>
        <v-icon large> mdi-phone-in-talk </v-icon>
        <p>{{ contact.phone_number }}</p>
      </v-card-subtitle>
      <v-card-subtitle>
        <v-icon large> mdi-cake </v-icon>
        <p>{{ contact.date_of_birth }}</p>
      </v-card-subtitle>
      <v-card-subtitle>
        <v-icon large> mdi-account </v-icon>
        <p>{{ contact.social_insurance_number }}</p>
      </v-card-subtitle>
    </v-card>
  </v-container>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue'
import { useRoute } from 'vue-router'
import { useContactById } from '../api/useContact'

// Components
import ToolBar from '../components/ToolBar.vue'

export default defineComponent({
  name: 'HomeView',

  components: {
    ToolBar,
  },
  setup() {
    const route = useRoute()
    const { isFetching, error, contact } = useContactById(
      Number(route.params.id)
    )
    return { isFetching, error, contact }
  },
})
</script>
