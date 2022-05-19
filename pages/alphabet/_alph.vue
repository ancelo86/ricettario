<template>
    <div>
        <div class="row">
            <div class="col-xl-12 mt-4">
                <h1>{{this.$route.params.alph}}</h1>
                <div>
                    <b-row >
                        <div class="col-xl-3" v-for="mealFinal in mealInfo" :key="mealFinal.id" >
                            <b-card class="m-1 title" bg-variant="dark" :title="`${mealFinal.nome}`" :img-src='`${mealFinal.img}`'>
                                <b-button :to='`/meals/${mealFinal.id}`' variant="primary">Vai</b-button>
                            </b-card>
                         </div>
                    </b-row>
                </div> 
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                meal: null,
                mealInfo: []

            };
        }, 
        async mounted() {
            try {
                let res = await this.$axios.$get(`https://www.themealdb.com/api/json/v1/1/search.php?f=${this.$route.params.alph}`);
                                   
                    this.meal= res.meals
                    this.meal.forEach(item => {
                        const {idMeal , strMeal, strMealThumb} = item
                        const temp ={idMeal , strMeal, strMealThumb}
                        this.mealInfo.push({id: idMeal, nome:strMeal, img:strMealThumb})
                    });
                    // for(let i=0; i<this.meal.length; i++){
                    //     let nome = this.meal[i].strMeal
                    //     let id= this.meal[i].idMeal                            
                    //     let img= this.meal[i].strMealThumb
                    //     this.mealInfo.push({nome , id , img})
                    // }       
                
            } 
            catch (error) {
                console.log(error);
            }
        },
    };

</script>

<style>



</style>
