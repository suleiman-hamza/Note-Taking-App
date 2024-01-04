<script setup>
import { reactive, onMounted } from 'vue'
import InputComponent from './components/InputComponent.vue'

const notes = reactive([])
const timestamps = reactive([])

const handleEvent = (event) => {
  notes.push(event.note);
  timestamps.push(event.timeStamp);

  localStorage.setItem('notes', JSON.stringify(notes))
  localStorage.setItem('timestamps', JSON.stringify(timestamps))
}

onMounted(() => {
  const not = localStorage.getItem('notes')
  if (not) {
    notes = not
  }
})
</script>

<template>
    <div class="notes-section">
      <div class="columns">
        <div class="column has-text-centered">
          <strong>Notes</strong>
          <div class="notess" v-for="items in notes">
            {{ items }}
          </div>
        </div>
        <div class="column has-text-centered">
          <strong>Timestamp</strong>
          <div class="timestamps" v-for="time in timestamps">
            {{ time }}
          </div>
        </div>
      </div>
      <InputComponent @monitorEvent="handleEvent" />
    </div>
</template>

<style scoped>
  .notes-section {
    border: 1px solid black;
    padding: 1.5rem
  }
  .columns {
    display: flex;
    margin-bottom: 2rem;
    width: 600px;
    justify-content: space-between;
  }
  .column {
    border: 1px solid red;
    padding: 1rem;
    width: 100%;
    text-align: center;
  }
</style>
