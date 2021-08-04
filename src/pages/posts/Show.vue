<template>

          <div class="col-md-4 my-2" >
            <div class="card">
            <div class="card-header">
                 {{ post.title }}
             </div>
              <ul class="list-group list-group-flush">
                <li class="list-group-item">Body: {{ post.body }}</li>
              </ul>
              <div class="card-footer">
                <router-link class="btn btn-sm btn-success" :to="{name:'editPost' , params:{id:post.id}}">Edit</router-link>
                <button class="btn btn-sm btn-danger ml-3">Delete</button>
              </div>
            </div>
          </div>

</template>

<script>
import axios from 'axios'
import { ref } from '@vue/reactivity';
import { useRoute } from 'vue-router';

export default {
    setup(){
        const post = ref([]);
        const route = useRoute()

        function getPost(){
            axios
            .get(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`)
            .then(function(response){
                post.value = response.data;
            })
            .catch(function(error){
                console.log(error)
            });
        }
        getPost()
        return {post, route};
    },

}
</script>

<style>

</style>