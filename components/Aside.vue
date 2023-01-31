<template>
  <div class="col-md-4">
    <div class="card my-4">
      <h5 class="card-header">Теги</h5>
      <div class="card-body">
        <div class="d-flex flex-wrap">
          <span v-for="tag in tags.results">
                    <nuxt-link :to="`/tags/${tag.url}`" class="mr-1 badge badge-info">#{{ tag.name }}</nuxt-link>
          </span>
        </div>
      </div>
    </div>

    <div class="card my-4">
      <h5 class="card-header">Последние статьи</h5>
      <div class="card-body" v-for="post in aside" :key="post.id">
        <nuxt-link :to="`/posts/${post.slug}`" class="card-link"><h5 class="card-title">{{post.title}}</h5></nuxt-link>
        <img :src="post.image" alt="" class="card-img-top">
        <h5>{{ post.h1 }}</h5>
        <div v-html="post.description" class="truncate"></div>
        <hr>
      </div>
    </div>
  </div>
</template>
  
  <script>
    export default {
      name: "Aside.vue",
      props: ['tags', 'aside']
    }
  </script>

  <style scoped>
  
  </style>