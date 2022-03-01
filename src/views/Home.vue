<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Suspense>
      <template #default>
        <Users />
      </template>
      <template #fallback>
        Loading data...
      </template>
    </Suspense>
  </div>
</template>

<script>
// @ is an alias to /src
import Users from '@/components/Users.vue'

export default {
  name: 'Home',
  components: {
    Users
  }
}
</script>
