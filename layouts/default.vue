<template>
    <div>
      <Navbar />
      <Slider />
      <div class="container">
        <Nuxt />
      </div>
      <Footer />
    </div>
  </template>
  
  
  <script>
  import Navbar from "~/components/navbar";
  import Slider from "~/components/slider";
  import Footer from "@/components/footer";
  
  export default {
    components: {
      Footer,
      Slider,
      Navbar,
    }
  };
  </script>
  
  <style>
  
  </style>