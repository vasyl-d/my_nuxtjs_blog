<template>
  <!-- Slider with images -->
  <div class="container-fluid home-slider">
    <div id="carouselExampleCaptions" class="carousel slide" data-ride="carousel" > 
        <ol class="carousel-indicators">
            <li data-target="#carouselExampleCaptions" data-slide-to="0" class="active"></li>
            <li data-target="#carouselExampleCaptions" data-slide-to="1"></li>
            <li data-target="#carouselExampleCaptions" data-slide-to="2"></li>
        </ol>
        <div class="carousel-inner">
            <div class="carousel-item active">
                <img src="img/Orderry_1.jpg" class="d-block w-100" alt="Наша команда">
                <div class="carousel-caption d-md-block intro-heading ">
                    <h5>Наша команда</h5>
                    <p>Могучий Support Orderry team</p>
                </div>

            </div>
            <div class="carousel-item">
                <img src="img/Orderry_2.jpg" class="d-block w-100" alt="Это я">
                <div class="carousel-caption d-md-block intro-heading ">
                    <h5>Это я</h5>
                    <p>Наверное всерстал какой-то крутой документ для клиента</p>
                </div>
            </div>
            <div class="carousel-item">
                <img src="img/Orderry_3.jpg" class="d-block w-100" alt="Творческий процесс">
                <div class="carousel-caption d-md-block intro-heading ">
                    <h5>Творческий процесс</h5>
                    <p>Не всегда все проходит на изи</p>
                </div>
            </div>
        </div>
        <a class="carousel-control-prev" href="#carouselExampleCaptions" role="button" data-slide="prev">
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
            <span class="sr-only">Previous</span>
        </a>
        <a class="carousel-control-next" href="#carouselExampleCaptions" role="button" data-slide="next">
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
            <span class="sr-only">Next</span>
        </a>
    </div>
    </div>
</template>
  
  <script>
  export default {
    name: "Slider"
  }
  </script>
  
  <style scoped>
  
  </style>