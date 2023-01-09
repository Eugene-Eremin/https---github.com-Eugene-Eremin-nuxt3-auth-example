<template>
    <div>
        <h1>Protected Page</h1>
    </div>
</template>

<script setup lang="ts">
    useHead({
        title: 'Protected'
    })

     definePageMeta({
        middleware: 'authenticated',
        layout: 'profile'
    })
</script>