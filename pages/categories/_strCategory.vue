<template>
<div>
  <div>
    <h1>{{this.$route.params.strCategory}}</h1>
  <b-row v-for="meals in strCategory" :key="meals.id">
    <div class="col-xl-3" v-for="mealsItem in meals" :key="mealsItem.id" >
  <b-card class="m-1" bg-variant="dark" text-variant="white" :title='`${mealsItem.strMeal}`' :img-src='`${mealsItem.strMealThumb}`'>
     <b-button :to='`/meals/${mealsItem.idMeal}`' variant="primary">Vai</b-button>
   <!-- <b-button @click="dettagliocliente(cliente, i)">Dettagli</b-button> -->
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
      strCategory: [],

    };
  },
  async mounted() {
    try {
      this.strCategory = await this.$axios.$get(`https://www.themealdb.com/api/json/v1/1/filter.php?c=${this.$route.params.strCategory}`);
      console.log(this.strCategory.meals);
      console.log(this.$route.params.strCategory)
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>



</style>
