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
                <router-link class="btn btn-sm btn-success" :to="{name:'editPost' , params:{id:post.id}}">
                    Edit
                </router-link>
                <button @click="deletePost" class="btn btn-sm btn-danger ml-3">
                    Delete
                </button>
              </div>
            </div>
          </div>

</template>

<script>
import axios from 'axios'
import { ref } from '@vue/reactivity';
import { useRoute } from 'vue-router';
import Swal from "sweetalert2";

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

      function deletePost() {
      axios
        .delete(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`)
        .then(function () {
          Swal.fire({
            title: "Thanks!",
            text: `Post (${route.params.id}) deleted successfully`,
            icon: "warning",
            confirmButtonText: "Ok",
          });
        })
        .catch(function (error) {
          console.log(error);
        });
    }
        return {post, route, deletePost};
    },

}
</script>

<style>

</style>