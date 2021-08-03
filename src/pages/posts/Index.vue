<template>
  <div class="col-lg-12 mb-3">
     <router-link class="btn btn-success" :to="{ name: 'createPost'}">Create Post</router-link>
  </div>
  <div class="col-md-4 my-2" v-for="post in posts" :key="post.id">
    <div class="card">
    <div class="card-header">
        <router-link :to="{ name : 'postId' , params :{ id : post.id }}">
          {{ post.title }}
        </router-link>
      </div>
      <ul class="list-group list-group-flush">
        <li class="list-group-item">Body: {{ post.body }}</li>
      </ul>
    </div>
  </div>

</template>

<script>
import axios from 'axios'
import { ref } from '@vue/reactivity';


export default {
    setup(){
        const posts = ref([]);

        function getPosts(){
            axios
            .get("https://jsonplaceholder.typicode.com/posts")
            .then(function(response){
                posts.value = response.data;
            })
            .catch(function(error){
                console.log(error)
            });
        }
        getPosts()
        return {posts};
    },

}
</script>

<style>

</style>