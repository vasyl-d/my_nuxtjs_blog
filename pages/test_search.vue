<template>
  <div>
  <Header :title=title />
  <div class="container">
    <div>
      <div class="row">
        <div class="col-lg-12">
          <nav aria-label="breadcrumb" class="mt-4">
            <ol class="breadcrumb">
              <li class="breadcrumb-item"><nuxt-link to="/">Главная</nuxt-link></li>
              <li class="breadcrumb-item active" aria-current="page">Поиск</li>
            </ol>
          </nav>
          <p class="lead">Найдено записей: {{count}}</p>
          <div class="row">
            <div v-for="post in posts" :key="post.slug" class="col-md-4">
                <div class="card mb-4 shadow-sm">
                  <img :src="post.image" alt="" class="card-img-top">
                  <div class="card-body">
                    <nuxt-link :to="`/posts/${post.slug}`" ><h4 class="card-title">{{ post.title }}</h4></nuxt-link>
                    <h5>{{ post.h1 }}</h5>
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
    </div>
  </div>
  </div>
</template>
  
   
 <script>
    import axios from "axios";
    import Header from "@/components/Header";
    export default {
      name: 'test_search',
      components: {Header},
      layout: "post_detail",
      watchQuery: ['q'],
      data() {
        return {
          count: 0,
          posts: [],
          title: '',
          next: '',
          previous: '',
        }
      },
      async asyncData({route}) {
        let q = route.query.q !== undefined ? `${route.query.q}` : '';
        const { data } = await axios.get(`http://127.0.0.1:8000/api/posts/?search=${q}`);
        return {
          count: data.count,
          posts: data.results,
          title: q,
          next: data.next,
          previous: data.previous,
        }
      },
      methods: {
        async fetch(page) {
          let q = this.q;
          const { data } = await axios.get(`http://127.0.0.1:8000/api/posts/?search=${q}${page}`);
          this.posts = data.results;
          this.next = data.next;
          this.previous = data.previous;
        },
      }
    }
    </script>