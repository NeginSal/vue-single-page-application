<template>
  <div>
      <h1>
          users
      </h1>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    setup(){
        function getUsers(){
            axios
            .get("https://jsonplaceholder.typicode.com/users")
            .then(function(response){
                console.log(response);
            })
            .catch(function(error){
                console.log(error)
            });
        }
        getUsers()
    },

}
</script>

<style>

</style>