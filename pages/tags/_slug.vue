<template>
  <div>
    <Header :title=url />
  <div class="container">
    <h1 class="my-3">Записи блога c тегом {{ url }}</h1>
    <div class="row">
      <div v-for="post in posts" :key="post.slug" class="col-md-4">
          <div class="card mb-4 shadow-sm">
            <img :src="post.image" alt="" class="card-img-top">
            <div class="card-body">
              <nuxt-link :to="`/posts/${post.slug}`" ><h4 class="card-title">{{ post.h1 }}</h4></nuxt-link>
              <div v-html="post.description"></div>
              <div class="mb-2">
              <span v-for="tag in post.tags">
                <nuxt-link :to="`/tags/${tag.url}`" class="mr-1 badge badge-info">#{{ tag.name }}</nuxt-link>
              </span>
              </div>
              <div class="d-flex justify-content-between align-items-center">
                <div class="btn-group">
                  <nuxt-link :to="`/posts/${post.slug}`" class="btn btn-sm btn-outline-secondary">Подробнее</nuxt-link>
                </div>
                <small class="text-muted">{{ post.created_at }}</small>
              </div>
            </div>
          </div>
      </div>
    </div>
  </div>
  </div>
</template>
  
<script>
import axios from "axios";
import post_detail from "@/layouts/post_detail";
import Header from "~/components/Header";
export default {
  components: {
    Header
  },
  layout: "post_detail",
  async asyncData({params}) {
    const { data } = await axios.get(`http://127.0.0.1:8000/api/tags/${params.slug}`);
    return {
      posts: data.results,
      url: params.slug
    }
  },
}
</script>

<style scoped>

</style>