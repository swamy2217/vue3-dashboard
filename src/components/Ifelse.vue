<script>
export default {
    name: 'if-else',
    data() {
        return {
            display: true,
            show: false,
        };
    },
}
</script>

<template>
    <h2>If else condition</h2>
    <div v-if="display">if block</div>
    <div v-if="!display">else block</div>
    <button type="button" @click="display = !display">click here</button>

</template>