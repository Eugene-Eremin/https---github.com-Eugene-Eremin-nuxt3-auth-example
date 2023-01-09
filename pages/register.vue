<template>
    <div>
        <h1>Register Page</h1>
        <form @submit.prevent="register">
            <input v-model="creadentials.email" type="email" placeholder="Email"/>
            <input v-model="creadentials.password" type="password" placeholder="Password"/>
            <button type="submit">Register</button>
        </form>
    </div>
</template>

<script setup>
    useHead({
        title: 'Register'
    })

    definePageMeta({
        middleware: 'unauthenticated'
    })
    
    const supaAuth = useSupabaseAuthClient().auth

    const creadentials = reactive({
        email: '',
        password: ''
    })

    const register = async () => {
        const { error } = await supaAuth.signUp(creadentials)

        if (error) {
            alert(error.message)
        } else {
            return navigateTo('/')
        }
    }
</script>

<style scoped>

</style>