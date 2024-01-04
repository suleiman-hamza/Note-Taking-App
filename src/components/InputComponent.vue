<template>
    <input 
        v-model="input" 
        type="text" 
        v-on:keyup.enter="addNote"
        placeholder="Enter Note Here" />
</template>

<script setup>
    import { ref } from 'vue';

    const props = defineProps(['placeholder'])
    const emit = defineEmits(['monitorEvent']);

    const input = ref('');
    const addNote = () => {
        emit('monitorEvent', {
            note: input.value,
            timeStamp: new Date().toLocaleString()
        });
        input.value = ''
    }

</script>
<style scoped>

</style>