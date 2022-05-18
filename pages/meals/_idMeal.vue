<template>
<div v-if="meal">
    <div class="row">
    <div class="col-xl-12 mt-4 ">
    <h1>{{meal.strMeal}}</h1>
        <b-card :img-src='`${meal.strMealThumb}`' img-alt="Card image" img-left>
        <b-card-text>
          <b-table-simple borderless outlined striped responsive>
              <b-thead>
                <b-tr>
                  <b-th>Ingrediente</b-th>
                  <b-th>Quantità</b-th>
                </b-tr>
              </b-thead>
              <b-tbody>
                <b-tr v-for="(ingrediente) in meal.listaIngredienti" :key="ingrediente.id">
                  <b-td>{{ingrediente.ingrediente}}</b-td>
                  <b-td>{{ingrediente.quantità}}</b-td>
                </b-tr>
              </b-tbody>
          </b-table-simple>
        </b-card-text>
      </b-card>
    </div>
    
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
      meal: null,

    };
  },
  async mounted() {
    try {
      let res = await this.$axios.$get(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${this.$route.params.idMeal}`);
      if(res && res.meals){
        this.meal= res.meals[0]
        this.meal.listaIngredienti=[]
        for(let i=1; i<=20; i++){
            let nome = this.meal['strIngredient' + i]
            // console.log(nome)
            let capacita = this.meal['strMeasure' + i]
            // console.log(capacita)
            if(nome && capacita)
            this.meal.listaIngredienti.push({ingrediente:nome, quantità:capacita })
}       
      }
      console.log(this.meal);
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>



</style>
