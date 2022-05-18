<template>
  <div>
    <div>
      <b-navbar type="dark" variant="dark">
        <b-navbar-brand v-b-toggle.sidebar-1>
          <img src="ricettario.jpg" class="d-inline-block align-top" width="40px" height="30px" alt="Kitten"/>Ricettario
        </b-navbar-brand>
        <div class="container-fluid">
          <form class="d-flex">
            <input class="form-control me-2" type="search" placeholder="Cerca" aria-label="Search"/>
            <button class="btn btn-outline-success" type="submit">Cerca</button>
          </form>
        </div>
      </b-navbar>
      <b-sidebar id="sidebar-1" title="Menu" shadow>
        <b-nav vertical class="w-25">
          <b-nav-item v-for="menu in vociMenu" :to="`${menu.to}`" :key="menu.i">{{ menu.label }}</b-nav-item>
        </b-nav>
      </b-sidebar>
    </div>
    <div class="row m-4">
      <div class="col-xl-1">
        <b-card class="p-1" v-for="(areas, i) in meals" :key="i" bg-variant="dark" text-variant="white"
         border-variant="dark" header="Area" header-bg-variant="dark" header-text-variant="white" align="center">
          <b-link :to="`/area/${area.strArea}`" v-for="(area, item) in areas" :key="item">
            <h6>{{ area.strArea }}</h6>
          </b-link>
        </b-card>
      </div>
      <div class="col-xl-10">
        <Nuxt />
      </div>
      <div class="col-xl-1">
        <b-card
          class="p-1"
          bg-variant="dark"
          text-variant="white"
          border-variant="dark"
          header="Ricerca per lettera"
          header-bg-variant="dark"
          header-text-variant="white"
          align="center"
        >
          <b-link
            :to="`/alphabet/${letter.lettera}`"
            v-for="(letter, item) in alphabet"
            :key="item"
          >
            <h6>{{ letter.lettera }}..</h6>
          </b-link>
        </b-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      alphabet: [],
      meals: [],
      vociMenu: [
        {
          label: "Home",
          to: "/",
        },
        {
          label: "Categorie",
          to: "/categories",
        },
        {
          label: "Area",
          to: "/area",
        },
      ],
    };
  },
  async mounted() {
    try {
      this.meals = await this.$axios.$get(`https://www.themealdb.com/api/json/v1/1/list.php?a=list`);
      console.log(this.meals);
      for (let i = 65; i <= 90; i++) {
        let lettera = String.fromCharCode(i);
        this.alphabet.push({ lettera });
      }
      console.log(this.alphabet);
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>
</style>