<template>
  <div class="home">    
    <section id="intro">
      <div class="container">
        <filterForm :filterData="filterData"></filterForm>
      </div>
      
      
          <div class="overVideo">
        </div>    
          <video autoplay muted loop id="carsVideo">
              <source src="@/assets/carsbg.mp4" type="video/mp4">
              Your browser does not support HTML5 video.
          </video>    
    </section>

    <section id="results" class="pt-5">            
            <div class="container">
                    <h1>Search car</h1>
                <div class="row">
                    <div class="col-12">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th scope="col"></th>
                                    <th scope="col">Brand</th>
                                    <th scope="col">Model</th>
                                    <th scope="col">Engine</th>
                                    <th scope="col">Price</th>
                                    <th scope="col">Action</th>
                                </tr>
                            </thead>
                            <tbody id="tbody_cars">
                              <car v-for="c in cars" :car="c" :CARS="cars" :key="c._id"></car>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </section>

  </div>
</template>

<script>
// @ is an alias to /src

import car from '@/components/Car.vue'
import filterForm from '@/components/HomeElements/FilterForm.vue'

export default {
  components: {
        car, filterForm
  },
  data(){
    return{
      filterData: {
          selected_brand: "",
          brands: [],
          selected_model: "",
          models: [],
          selected_engine:0,
          engines:[],
          price_min:0,
          price_max:0
      },
      cars: []
    }
  },
  created(){
    fetch("http://localhost:5001/api/cars").then(response => response.json()).then(json=>{
      console.log(json);
      this.cars = json;
    })
  },
  methods:{
    printMessage: function(msg){
      console.log(msg);
    }
  }
}
</script>

<style scoped lang="scss">
#carsVideo{
    width:100%;
}

#intro{
    position: relative;

    overflow: hidden;
}

#carsVideo{
    position: absolute;
    top:-105px;
    z-index: 45;
    
}

.overVideo{
    height:300px;
    background: orange;
    opacity: 0.25;
    overflow-x: hidden;
    z-index: 50;
}

.pageHeader{
      //background: url("./assets/header_bg.png");
}

#mainSearchForm{
  position: relative;
  z-index:1000;
  padding-top:60px;
}
</style>
