<!-- <script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue'
</script> -->
<!-- <script setup lang="ts"></script> -->
<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import type { Event } from '@/types'
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService'
import StudentService from '@/services/StudentService'

const events = ref<Event[]>(null)

onMounted(() => {
  EventService.getEvents()
    .then((response) => {
      events.value = response.data
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
    StudentService.getEvents()
    .then((response) => {
      events.value = response.data
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
})
</script>
<template>
  <h1>Events For Good</h1>
  <!-- new element -->
  <!-- <main>
    <TheWelcome />
  </main> -->
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
