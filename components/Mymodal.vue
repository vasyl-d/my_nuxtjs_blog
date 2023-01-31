<template>

<!-- The Modal -->
<div class="modal-overlay" @click="$emit('close-modal')">
  <div class="modal-dialog modal-dialog-centered" @click.stop>
    <div class="modal-content">

      <!-- Modal Header -->
      <div class="modal-header">
        <h4 class="modal-title">Пожалуйста укажите логин и пароль</h4>
        <button type="button" class="close" @click="$emit('close-modal')">&times;</button>
      </div>

      <!-- Modal body -->
      <div class="modal-body">
        <div class="text-center">
        <form class="form-signin" @submit.prevent="userLogin">
          <label for="inputUsername" class="sr-only">Имя пользователя</label>
          <input id="inputUsername" class="form-control" placeholder="Имя пользователя" required="" v-model="login.username">
          <label for="inputPassword" class="sr-only">Пароль</label>
          <input type="password" id="inputPassword" class="form-control mt-2" placeholder="Пароль" required="" v-model="login.password">
          <!-- Modal footer -->
          <div class="modal-footer">
            <button class="btn mt-2 btn-lg btn-primary btn-block" type="submit">Войти</button>
          </div>
        </form>
      </div>
      </div>

    </div>
  </div>
</div>
</template>

<script>
export default {
    name: "Mymodal",
    data() {
      return { 
        login: {
        username: '',
        password: '',
      },
      }
    },
    methods: {
    async userLogin() {
      try {
        let response = await this.$auth.loginWith('local', { data: this.login })
        console.log(response)
        this.$emit('close-modal')
      } catch (err) {
        console.log(err)
      }
    }
  }
  }
</script>

<style scoped>

</style>