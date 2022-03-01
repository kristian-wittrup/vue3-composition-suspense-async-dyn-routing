<template>

  <div>
    <p v-for="user in state.users" :key="user.id">
      
      <router-link :to="{
        name: 'UserDetails',
        params: {
          id: user.id
        }
      }" >
        {{user.first_name}}
      </router-link>
      <router-view></router-view>
    </p>
  </div> 
</template>

<script>
import { reactive, onMounted } from 'vue'


export default {
  async setup () {

    const state = reactive({
      users: null,
      error: null
    })

    const load = async() => {
      try {
        const usersResponse = await fetch("https://reqres.in/api/users")
        await usersResponse.json().then(userData => {
          state.users = userData.data
        })
      }

      catch(err) {
        state.error = err.message
        console.log(err)
      }
}
//await load();

 onMounted(() => {
  load()
})

    return {
      state
    }
  }
 
}
</script>

<style lang="scss" scoped>

</style>