<template>
    <div class="container mt-5">
      <div class="row " >
          <div class="col-md-4 my-2" v-for="user in users" :key="user.id">
              <UserCardView :user="user"/>
          </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
import { ref } from '@vue/reactivity';
import UserCardView from '@/components/users/CardView'

export default {
    components:{
       UserCardView
    },
    setup(){
        const users = ref([]);

        function getUsers(){
            axios
            .get("https://jsonplaceholder.typicode.com/users")
            .then(function(response){
                users.value = response.data;
            })
            .catch(function(error){
                console.log(error)
            });
        }
        getUsers()
        return {users};
    },

}
</script>

<style>

</style>