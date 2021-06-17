<template>
  <div class="currencies">
    <div class="row d-flex justify-content-center ">
      <div class="" v-for="c in cryptos" :key="c.id">
        <div class="col-3">
          <div class="card mb-5" style="width: 18rem">
            <img class="card-img-top" :src="c.logo_url" alt="Logo" style="height:300px;max-width:300px;" />
            <div class="card-body">
              <h5 class="card-title">{{c.name}}</h5>
              <p class="card-text">
                $ <strong>{{c.price}}</strong> USD
              </p>
			  <p class="card-text">
				{{c.price_date}}
			  </p>              
            </div>
          </div>

        </div>
      </div>
    </div>

	<nav aria-label="Page navigation example">
  <ul class="pagination justify-content-center">
    <li class="page-item ">
      <a class="page-link" href="" @click="cambiarPagina( this.page = this.page > 1 ? (this.page-1) : 1 )"> Anterior </a>
    </li>
	<div v-for="p in pages" :key="p" :to="{name: 'Currencies', params: {pagina:p}}">
		<li class="page-item"><p class="page-link" @click="cambiarPagina(p)" href="#">{{p}}</p></li>
	</div>
    <li class="page-item">
      <a class="page-link" href="" @click="cambiarPagina( this.page = this.page < 6 ? (this.page+1) : 6 )"> Siguiente </a>
    </li>
  </ul>
</nav>

  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Currencies",
  data: () => ({
    cryptos: [],    
	page: 1,
	pages: [1,2,3,4,5,6]
  }),
    methods: {
	  cambiarPagina(p) {
		  this.page = p
		   	   		  
   axios
      .get(
        `https://api.nomics.com/v1/currencies/ticker?key=1a2b63f7fe249f264cf860de3e9ff912838c5f1b&interval=1d,30d&per-page=16&page=${this.page}`
      )
      .then((response) => {
        this.cryptos = response.data;
      })
      .catch((e) => {
        console.log(e);
      });
	  window.scrollTo(0,0);			  
	  }
	  
  },
  created() {
	  this.page = this.$route.params.pagina
	  console.log(this.page)	  
	  this.cambiarPagina(this.page)
	  
  },
  props: {},
};
</script>

<style scoped>
</style>
