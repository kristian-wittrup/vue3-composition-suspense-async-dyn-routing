<template>
   <div>
    <!--   test with: {{ $route.params.id }}
      test prop with only: {{ id }} 
     <div v-if="!userDetails.length">
      id2 : {{userDetails.first_name}}
    </div>  
    <div v-else>
      loading
    </div>
 -->
     <Suspense>
      <template #default> 
        <div>
          <p>FirstName : {{userDetails.first_name}} {{userDetails.last_name}}</p>
          <p>Email: {{userDetails.email}}</p>
          <p>UserID: {{userDetails.id}}</p>
          <img :src="userDetails.avatar" height=100 alt="">
        </div>
      </template> 
      <template #fallback>>
        No data
      </template>
    </Suspense> 
    <button @click="goBack()">
      go back
    </button>
  </div>

</template>

<script>
import { ref } from 'vue'
// import router from '@/router' // allow use of router
import { useRoute, useRouter } from 'vue-router'


  export default {
    name: "UserDetails",
   // props: ['id'], // Props instead of returning (accept prop in router.js) // 2
    

  setup(/*props*/) {
    const router = useRouter() // To be able to use the router.go(-1)
    const route = useRoute() // For route.params.id
    const id = route.params.id // For route.params.id

    const error = ref(null); // with try & catch
    const userDetails = ref([]);

    const load = async () => {
      try {
        const usersResponse = await fetch("https://reqres.in/api/users/" + id + "?delay=3");
        // ;debugger
        await usersResponse.json().then(userData => {
          userDetails.value = userData.data 
          
        });
        //  console.log("testy users2", userDetails.value.id)
        
      }
      catch (err){
        error.value = err.message
        console.log(error.value)
      }
    }
    load()
    // console.log("testy prop", props.id) // For testing props.id is correct
    

    // go back stuff
    function goBack() { // remember to return it
      router.go(-1)
    }
    /* other way 
    const goBack = () => {
        router.go(-1)
      }
    */
    
  return { userDetails, error, goBack };

  
  },
 
    
}
</script>

<style lang="scss" scoped>

</style>