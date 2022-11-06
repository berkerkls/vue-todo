<template>
    <input type="text" @keydown.enter="enterInput" placeholder="What will you buy today?" />
</template>

<script>
    export default {
        inject: ["enterInput"]
    }
</script>