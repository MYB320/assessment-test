<template>
  <v-card hover @click="ShowDetails">
    <v-img :src="avatar" height="200px" cover></v-img>
    <v-card-title> {{ fname }} {{ lname }} </v-card-title>
    <v-card-subtitle>
      <v-icon large> mdi-email </v-icon>
      <p>{{ email }}</p>
    </v-card-subtitle>
  </v-card>
</template>

<script>
import { ref } from 'vue'
import router from '../router'

export default {
  name: 'CardItem',
  props: ['contact'],

  setup(props) {
    const fname = ref(props.contact.first_name)
    const lname = ref(props.contact.last_name)
    const email = ref(props.contact.email)
    const avatar = ref(props.contact.avatar)

    const ShowDetails = () => {
      router.push(`/contact/${props.contact.id}`)
    }

    return { fname, lname, email, avatar, ShowDetails }
  },
}
</script>

<style></style>
