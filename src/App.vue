<script setup>
import { ref, computed, reactive } from 'vue'
import InputComponent from './components/InputComponent.vue'

let notes = reactive([])
let timestamps = reactive([])
const placeholder = 'Enter a note';

const handleEvent = (event) => {
  notes.push(event.note);
  timestamps.push(event.timeStamp);
};
</script>

<template>
    <div class="notes-section">
      <div class="columns">
        <div class="column has-text-centered">
          <strong>Notes</strong>
          <div class="notess" v-for="items in notes">
            {{ notes }}
          </div>
        </div>
        <div class="column has-text-centered">
          <strong>Timestamp</strong>
          <div class="timestamps" v-for="time in timestamps">
            {{ timestamps }}
          </div>
        </div>
      </div>
      <InputComponent @monitorEvent="handleEvent" :placeholder="placeholder" />
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
