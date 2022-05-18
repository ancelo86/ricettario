<template>
<div class="container">
  <b-row v-for="(area,i) in meals" :key="i">
    <div class="col-xl-2" v-for="strArea in area" :key="strArea.i">
  <b-card class="m-1 title" bg-variant="dark" :title="`${strArea.strArea}`">
 <b-button :to='`/area/${strArea.strArea}`' variant="primary">Vai</b-button>

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
     meals: [],

    };
  },
  async mounted() {
    try {
      this.meals = await this.$axios.$get(`https://www.themealdb.com/api/json/v1/1/list.php?a=list`);
      console.log(this.meals);
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>

</style>