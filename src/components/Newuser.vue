<template>
    <div>
        <div>{{ data.name }}</div>
        <div>{{ data.email }}</div>
    </div>
</template>

<script>
    export default {
        name: 'new-user',
        props: {
            data: Object,
        },
    }
</script>