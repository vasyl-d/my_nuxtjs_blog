<template>
  <div>
      <Header :title=title />
      <div class="text-center">
        <form class="form-signin" @submit.prevent="userLogin">
          <label for="inputUsername" class="sr-only">Имя пользователя</label>
          <input id="inputUsername" class="form-control" placeholder="Имя пользователя" required="" v-model="login.username">
          <label for="inputPassword" class="sr-only">Пароль</label>
          <input type="password" id="inputPassword" class="form-control mt-2" placeholder="Пароль" required="" v-model="login.password">
          <button class="btn mt-2 btn-lg btn-primary btn-block" type="submit">Войти</button>
        </form>
      </div>
    </div>
</template>

<script>
import Header from "@/components/Header";
export default {
  layout: "post_detail",
  components: { Header },
  data() {
    return {
      login: {
        username: '',
        password: '',
      },
      title : 'Пожалуйста укажите логин и пароль',
    }
  },
  methods: {
    async userLogin() {
      try {
        let response = await this.$auth.loginWith('local', { data: this.login })
        console.log(response)
        this.$router.push('/')
      } catch (err) {
        console.log(err)
      }
    }
  }
}
</script>

<style scoped>

</style>