<template>
    <div>
        <h1>Profile</h1>
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
        <slot/>
    </div>
</template>

<script setup>
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
</script>

<style scoped>

</style>