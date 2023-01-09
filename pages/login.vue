<template>
    <div>
        <h1>Login Page</h1>
        <form @submit.prevent="login">
            <input v-model="creadentials.email" type="email" placeholder="Email"/>
            <input v-model="creadentials.password" type="password" placeholder="Password"/>
            <button type="submit">Login</button>
        </form>
    </div>
</template>

<script setup>
    useHead({
        title: 'Login'
    })

    definePageMeta({
        middleware: 'unauthenticated'
    })
    
    const supaAuth = useSupabaseAuthClient().auth

    const creadentials = reactive({
        email: '',
        password: ''
    })

    const login = async () => {
        const { data, error } = await supaAuth.signInWithPassword(creadentials)

        console.log('data', data)
        console.log('error', error)

        if (error) {
            alert(error.message)
        } else {
            return navigateTo('/')
        }
    }
</script>

<style scoped>

</style>