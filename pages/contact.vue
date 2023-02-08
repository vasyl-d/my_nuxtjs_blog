<template>
  <div>
    <Header :title=title />
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <nav aria-label="breadcrumb" class="mt-4">
            <ol class="breadcrumb">
              <li class="breadcrumb-item"><a href="">Главная</a></li>
              <li class="breadcrumb-item active" aria-current="page">Контакты</li>
            </ol>
          </nav>
          <p class="lead">Чтобы связаться со мной заполните форму обратной связи</p>
          <form name="contact-form">
            <div class="row">
              <div class="col-md-6">
                <div class="md-form mb-0">
                  <label for="name" class="sr-only">Ваше имя</label>
                  <input type="text" id="name" class="form-control" placeholder="Ваше имя" v-model="form.name" >
                </div>
              </div>
              <div class="col-md-6">
                <div class="md-form mb-0">
                  <label for="email" class="sr-only">Ваша почта</label>
                  <input type="email" id="email" class="form-control" required placeholder="Ваша почта" v-model="form.email" >
                </div>
              </div>
            </div>

            <div class="row mt-3">
              <div class="col-md-12">
                <div class="md-form mb-0">
                  <label for="subject" class="sr-only">Тема</label>
                  <input type="text" id="subject" class="form-control" placeholder="Тема" v-model="form.subject" >
                </div>
              </div>
            </div>

            <div class="row mt-3">
              <div class="col-md-12">
                <div class="md-form">
                  <label for="message" class="sr-only">Ваше сообщение</label>
                  <textarea type="text" id="message" rows="2" class="form-control md-textarea" placeholder="Ваше сообщение" v-model="form.message" ></textarea>
                </div>
              </div>
            </div>
          </form>
          <div class="text-center text-md-left mt-3">
            <button class="btn btn-primary" type="submit" @click.prevent="submitForm" :disabled='!isComplete'>Отправить</button>
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
  components: {Header},
  layout: "post_detail",
  name: "Contact",
  data() {
    return {
      title: "Написать мне",
      err: '',
      form: {
        name: '',
        email: '',
        subject: '',
        message: '',
      }
    }
  },
  methods: {
    async submitForm() {
      const data = {
          name: this.form.name,
          email: this.form.email,
          title: this.form.subject,
          message: this.form.message
        };
      const headers = {
          'Content-Type': 'application/json'
          };
      console.log('submitting data...');
      try {
        let response = await this.$axios.post('http://127.0.0.1:8000/api/feedback/', data, headers);
        this.$router.push("/success");
      } catch(err) {
        this.title = "Error request:";
        console.log(err);
      }
    },
    validEmail(email) {
      var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
  },
  computed: {
      isComplete () {
        return this.form.name && this.validEmail(this.form.email) && this.form.subject && this.form.message;
      },
    },
}
</script>

<style scoped>

</style>