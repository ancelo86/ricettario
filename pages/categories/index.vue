<template>
<div>
  <b-row v-for="category in categories" :key="category.id">
    <div class="col-xl-2" v-for="categoryId in category" :key="categoryId.id" >
  <b-card class="m-1 title" bg-variant="dark" :title="`${categoryId.strCategory}`" :img-src='`${categoryId.strCategoryThumb}`'>
 <b-button :to='`categories/${categoryId.strCategory}`' variant="primary">Vai</b-button>
  <!-- <b-button @click="dettagliocliente(cliente, i)">Dettagli</b-button> -->
</b-card>
  </div>
    </b-row>

</div>
</template>

<script>
export default {
  name: 'IndexPage',
    data() {
    return {
     categories: [],

    };
  },
  async mounted() {
    try {
      this.categories = await this.$axios.$get(`https://www.themealdb.com/api/json/v1/1/categories.php`);
      console.log(this.categories);
      console.log(this.$route)
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>

.title{
  
  color: white;
}

</style>
