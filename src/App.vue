<script setup>
import { onMounted, ref } from 'vue'
import InputComponent from './components/InputComponent.vue'

let notes = ref([])
let timestamps = ref([])

onMounted(() => {
  const retrieveString = localStorage.getItem('notes') || []
  const retrievedArray = JSON.parse(retrieveString)
  notes.value = retrievedArray

  const retrievedTimeStamp = localStorage.getItem('timestamped')
  const retrievedTime = JSON.parse(retrievedTimeStamp)
  timestamps.value = retrievedTime
})

const handleEvent = (event) => {
  notes.value.push(event.note);
  timestamps.value.push(event.timeStamp);

  handleSave();
}

function handleSave() {
  const stringifiedArray = JSON.stringify(notes.value)
  localStorage.setItem('notes', stringifiedArray)

  const stringifiedTimestamp = JSON.stringify(timestamps.value)
  localStorage.setItem('timestamped', stringifiedTimestamp)
}
</script>

<template>
    <div class="notes-section">
      <div class="columns">
        <div class="column has-text-centered">
          <strong>Notes</strong>
          <div class="notess" v-for="items in notes">{{ items }}</div>
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
