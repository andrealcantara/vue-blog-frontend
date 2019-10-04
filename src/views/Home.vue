<template>
  <div>
    <div class="text-center">
      <h1>Blog Tutorial</h1>
      <p>Aqui é um tutorial de um blog criado com Nest.Js VUE e MongoDB</p>
      <div v-if="posts.length === 0">
        <h2> Posts não encontrados no momento</h2>
      </div>
      <div class="row">
        <div class="col-md-4" v-for="post in posts" :key="post._id">
          <div class="card mb-4 shadow-sm">
            <div class="card-body">
              <h2 class="card-img-top"> {{ post.title }} </h2>
              <p class="card-text"> {{ post.body }} </p>
              <div class="d-flex justify-content-between align-items-center">
                <div class="btn-group" style="margin-bottom: 20px;">
                  <router-link :to="{name:'Post',params:{id:post._id}}" class="btn btn-sm btn-outline-secondary">Visualizar</router-link>
                  <router-link :to="{name:'Edit',params:{id:post._id}}" class="btn btn-sm btn-outline-secondary">Editar </router-link>
                  <button class="btn btn-sm btn-outline-secondary" v-on:click="deletePost(post._id)">Apagar</button>
                </div>
              </div>
              <div class="card-footer">
                <small class="text-muted">Postado em : {{ post.date_posted }} </small>
                <small class="text-muted">por: {{ post.author }}</small>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { server } from "@/utils/helper";
import axios from "axios";


export default {
  data() {
    return {
      posts: []
    };
  },
  created() {
    this.receberPosts();
  },
  methods:{
    receberPosts(){
      axios
        .get(`${server.baseURL}/blog/post`)
        .then(data => {
          this.posts = data.data
          });
    },
    deletePost(id) {
      axios.delete(`${server.baseURL}/blog?postID=${id}`).then(data => {
        console.log(data);
        window.location.reload();
      });
    }
  }
}
</script>