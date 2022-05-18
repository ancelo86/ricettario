<template>
<div>
  <div>
       <h1>{{this.$route.params.area}}</h1>
  <b-row v-for="selectedArea in area" :key="selectedArea.idMeal">
    <div class="col-xl-3" v-for="(areaItem,i) in selectedArea" :key="i" >
  <b-card class="m-1" bg-variant="dark" text-variant="white" :title='`${areaItem.strMeal}`' :img-src='`${areaItem.strMealThumb}`'>
     <b-button :to='`/meals/${areaItem.idMeal}`' variant="primary">Vai</b-button>
 </b-card>
  </div>
    </b-row>

</div>
   
</div>
</template>

<script>
export default {
  name: 'IndexPage',
    data() {
    return {
        imgsrc: '',
        title:'',
      area: [],

    };
  },
  async mounted() {
    try {
      this.area = await this.$axios.$get(`https://www.themealdb.com/api/json/v1/1/filter.php?a=${this.$route.params.area}`);
      console.log(this.area);
      console.log(this.$route.params)
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>



</style>
