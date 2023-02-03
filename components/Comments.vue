<template>
    <div>
      <div class="card my-4">
        <h5 class="card-header">Прокомментируй:</h5>
        <div class="card-body">
          <form @submit.prevent="addComment();">
            <div class="form-group">
              <textarea class="form-control" rows="3" v-model="message"></textarea>
            </div>
            <span v-if="user">
              <button type="submit" class="btn btn-primary" :disabled='!isComplete'>Отправить</button>
            </span>
            <span v-else>
              <h5>Залогиньтесь или зарегистрируйтесь для комментирования</h5>
            </span>
          </form>
        </div>
      </div>
      <div v-for="comment in comments" class="media mb-4">
        <img class="d-flex mr-3 rounded-circle" src="https://via.placeholder.com/50" alt="">
        <div class="media-body">
          <h5 class="mt-0">{{ comment.username }}</h5>
              {{ comment.text }}
        </div>
        <client-only >
          <span v-if="user">
            <span v-if="comment.username === user.username">
              {{ err }}
              <button class="btn btn-outline-success my-2 my-sm-0 mr-2" type="submit" @click.prevent="delComment(comment.id);">Удалить</button>
            </span>
          </span>
        </client-only>
      </div>
    </div>
  </template>
  
<script>
import axios from 'axios';
export default {
  name: "Comments.vue",
  props: ['comments', 'post'],
  data(){
    return {
      message: '',
      err: '',
    }
  },
  methods:{
    async delComment(id){
      try {
        let url = "http://localhost:8000/api/comments/delete/"+id;
        const headers = {
          "Authorization": `Bearer ${this.token}`
          };
        let response = await this.$axios.delete(url, headers);
        //need to delete comment from list on this.comments
        const comIndex = this.comments.findIndex(p => p.id === id)
        this.comments.splice(comIndex, 1)
      } catch (err) {
        this.err = err;
        console.log(err)
      }
    },
    async addComment(){
      const data = {
                post: this.$props.post.slug,
                username: this.user.username,
                text: this.message
              };
      const headers = {
          'Content-Type': 'application/json', 
          "Authorization": `Bearer ${this.token}`
          };
        try {  
          let response = await this.$axios.post('http://localhost:8000/api/comments/', data, headers);
          this.message = '';
          this.comments.splice(0, 0, response.data)
        } catch (err) {
          this.message = err;
        }
      }
    },
  computed: {
    loggedIn() {
      return this.$auth.loggedIn
    },
    user() {
      return this.$auth.user
    },
    isComplete () {
      return this.message;
    }
  }
}
</script>
  
  <style scoped>
  
  </style>