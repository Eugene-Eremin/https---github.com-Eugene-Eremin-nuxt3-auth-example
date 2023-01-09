<template>
    <div>
      <nav>
        <ul>
            <li>
                <NuxtLink to="/">Home</NuxtLink>
            </li>
            <template v-if="!user">
                <li>
                    <NuxtLink to="/login">Login</NuxtLink>
                </li>
                <li>
                    <NuxtLink to="/register">Register</NuxtLink>
                </li>
            </template>
            <template v-else>
                <li>
                    <NuxtLink to="/protected">Protected</NuxtLink>
                </li>
                <li>
                    <NuxtLink to="/second-protected">Second-protected</NuxtLink>
                </li>
                <li>
                    <NuxtLink @click="logout">Logout</NuxtLink>
                </li>
            </template>
        </ul>
      </nav>
      <slot />
    </div>
  </template>
  
  <script setup lang="ts">
    const user = useSupabaseUser()
    
    const supaAuth = useSupabaseAuthClient().auth
  
    const logout = async () => {
        const { error } = await supaAuth.signOut()
        if (error) {
            alert(error.message)
        } else {
            return navigateTo('/login')
        }
    }

    // Можно использовать этот способ, если мы хотим повесить middleware на какой то layout
    // https://stackoverflow.com/questions/73293352/nuxt-3-how-to-use-route-middleware-in-a-layout-can-i?newreg=02a0735e11b84cadac52aa3eeb321f07
    // export default defineNuxtRouteMiddleware((to, from) => {
    //     const user = useUserStore();
    
    //     if (!user && to.meta.layout === auth) {
    //         return navigateTo("/login");
    //     }
    // });
  </script>