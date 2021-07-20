<template>
          <div class="col-md-4 my-2">
              <UserCardView :user="user"/>
          </div>

</template>

<script>
import axios from 'axios'
import { ref } from '@vue/reactivity';
import UserCardView from '@/components/users/CardView'
import { useRoute } from "vue-router";

export default {
    components:{
       UserCardView
    },
    setup(){
        const user = ref({});
        const route = useRoute();

        function getUser(){
            axios
            .get(`https://jsonplaceholder.typicode.com/users/${route.params.id}`)
            .then(function(response){
                user.value = response.data;
            })
            .catch(function(error){
                console.log(error)
            });
        }
        getUser()
        return {user};
    },

}
</script>

<style>

</style>