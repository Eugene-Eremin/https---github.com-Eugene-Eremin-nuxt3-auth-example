<template>
    <div>
        <h1>Second-protected Page</h1>
    </div>
</template>

<script setup lang="ts">
    useHead({
        title: 'Second-protected'
    })

    definePageMeta({
        middleware: 'authenticated',
        layout: 'profile'
    })
</script>