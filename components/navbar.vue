<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark sticky-top">
    <Mymodal v-show="showModal" @close-modal="showModal = false" />
    <nuxt-link class="navbar-brand" to="/">
      <img src="https://upload.wikimedia.org/wikipedia/commons/c/c3/Python-logo-notext.svg" width="30" height="30" alt="logo">
    </nuxt-link>
    <button class="navbar-toggler" type="button" data-toggle="collapse"
            data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <nuxt-link class="nav-link" to="/">Главная</nuxt-link>
        </li>
        <li class="nav-item ">
          <nuxt-link class="nav-link" to="/contact">Контакты</nuxt-link>
        </li>
      </ul>
      <form class="form-inline my-2 my-lg-0">
        <input name="q" v-model="q" type="text" class="form-control mr-sm-2" placeholder="Поиск" aria-label="Поиск">
        <button class="btn btn-outline-success my-2 my-sm-0 mr-2" type="submit" @click.stop.prevent="submit()">Поиск</button>
      </form>
      <client-only>
        <span class="navbar-text mr-2" v-if="user">Hello, {{ user.username }}</span>
        <span v-if="loggedIn"><button class="btn btn-outline-light mr-2" @click="logOut();">Выход</button></span>
        <span v-else>
          <button class="btn btn-outline-success my-2 my-sm-0 mr-2" @click="showModal = true">Вход</button>
          <nuxt-link class="btn btn-outline-light mr-2" to="/signup">Регистрация</nuxt-link>
        </span>
      </client-only>
    </div>
  </nav>
</template>

<script>
import Mymodal from "@/components/Mymodal";
export default {
  name: "Navbar",
  components: { Mymodal },
  data(){
    return {
      q : null,
      showModal: false,
    }
  },
  methods: {
    submit(){
      this.$router.push("/search?q="+this.q);
    },
    async logOut() {
      await this.$auth.logout()
  }
  },
  computed: {
    loggedIn() {
      return this.$auth.loggedIn
    },
    user() {
      return this.$auth.user
    }
  }
}
</script>

<style scoped>

</style>