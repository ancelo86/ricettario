<template>
<div>
<template>
<div>
  <h1>Italian Food</h1>
  <div>
  <b-row v-for="meals in italianFood" :key="meals.id">
  <div class="col-xl-2" v-for="mealsItem in meals" :key="mealsItem.id" >
  <b-card class="m-1" bg-variant="dark" text-variant="white" :title='`${mealsItem.strMeal}`' :img-src='`${mealsItem.strMealThumb}`'>
  <b-button>Dettagli</b-button>
</b-card>
  </div>
    </b-row>

</div>
  
</div>
</template>

</div>
</template>

<script>
export default {
  name: 'IndexPage',
    data() {
    return {
        imgsrc: '',
        title:'',
      italianFood: [],
      

    };
  },
  async mounted() {
    try {
      this.italianFood = await this.$axios.$get(`https://www.themealdb.com/api/json/v1/1/filter.php?a=Italian`);
      // console.log(this.italianFood);

    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>



</style>