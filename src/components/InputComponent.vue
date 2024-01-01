<template>
    <input 
        v-model="input" 
        type="text" 
        v-on:keyup.enter="addNote"
        :placeholder="placeholder" />
</template>

<script setup>
    import { ref } from 'vue';

    const props = defineProps(['placeholder'])
    const emit = defineEmits(['monitorEvent']);

    let input = ref('')
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