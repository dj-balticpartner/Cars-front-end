<template>
<div id="mainSearchForm">
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">Car search</h5>
            <div class="row">
                <div class="col-lg-4">                
                <div class="form-group">
                    <label for="exampleFormControlSelect1">Brand</label>
                    <select class="form-control" id="exampleFormControlSelect1" @change="brandSelectChange()" v-model="this.filterData.selected_brand">                        
                        <option value="" selected disabled>-select brand-</option>
                        <option v-for="br in this.filterData.brands" :key="br">{{br}}</option>
                    </select>
                    </div>
                </div>
                <div class="col">
                
                </div>
            </div>
            
            <a href="#" class="btn btn-primary">Filter</a>
        </div>
    </div>
</div>
</template>
<script>
export default {
  props: ["filterData"], // filters
  name: "FilterForm",
  data() {
    return {};
  },
  created() {
    this.filterData.brands = [];
    fetch("http://localhost:5001/api/cars/filter/brands")
      .then(response => response.json())
      .then(json => {
        this.filterData.brands = json;
      });
  },
  computed() {},
  methods: {
    brandSelectChange() {
        console.log(this.key)
    }
  }
};
</script>