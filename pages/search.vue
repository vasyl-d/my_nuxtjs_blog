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
          <nav aria-label="Paginate me">
            <ul class="pagination justify-content-center" >
              <button v-if="previous != null" class="page-link" @click="fetchPost(previous);" tabindex="-1">Предыдущая</button>
              <li v-else class="page-item disabled">
                <a class="page-link disabled" href="#" tabindex="-1">Предыдущая</a>
              </li>
              <span v-for="i in total">
                <li  v-if="current_page === i || ($route.query.page === '/' && i === 1)" class="page-item active">
                  <button class="page-link" @click="fetchPost(i);">{{i}}</button></li>
                <li v-else class="page-item">
                  <button class="page-link" @click="fetchPost(i);">{{i}}</button></li>
              </span>
              <button v-if="next != null" class="page-link" @click="fetchPost(next);">Следующая</button>
              <li v-else class="page-item disabled">
                <a class="page-link" href="#">Следующая</a>
              </li>
            </ul>
          </nav>
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
          posts: [],
          title: '',
          total:0,
          next: 1,
          previous: 1,
          current_page: 1,
          count:0,
        }
      },
      async asyncData({route}) {
        let q = route.query.q !== undefined ? `${route.query.q}` : '';
        const { data } = await axios.get(`http://127.0.0.1:8000/api/posts/?search=${q}`);
        let total = Math.ceil(data.count / 6)
        let next = data.next != null ? 2 : data.next;
        let previous = data.previous != null ? 1 : data.previous;
        return {
          posts: data.results,
          total: total,
          next: next,
          previous: previous,
          current_page: 1,
          count: data.count,
          title:q
        }
      },
      methods: {
      async fetchPost(i) {
          let page1 = i >= 1 ? i : 1;
          const { data } = await axios.get(`http://127.0.0.1:8000/api/posts/?search=${this.title}&page=${page1}`);
          this.posts = data.results;
          this.next = data.next != null ? i+1 : data.next;
          this.previous = data.previous != null ? i-1 : data.previous;
          this.current_page = i;
          this.total = Math.ceil(data.count / 6);
        },
      },
    }
    </script>