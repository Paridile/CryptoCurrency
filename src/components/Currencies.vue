<template>
  <div class="currencies">
        <p>{{ax}}</p>
    <div class="row d-flex justify-content-center">
      <div class="" v-for="c in cryptos" :key="c.id">
        <div class="col-3">
          <div class="card  text-white bg-dark mb-4" style="width: 18rem">
            <img
              class="card-img-top custom-dark p-5"
              :src="c.logo_url"
              alt="Logo"
              style="height: 300px; max-width: 300px"
            />
            <div class="card-body custom-dark">
              <h5 class="card-title">{{ c.name }}</h5>
              <p class="card-text">
                $ <strong>{{ c.price }}</strong> USD
              </p>
              <p class="card-text">
                {{ c.price_date }}
              </p>
              <a class="btn custom-btn btn-primary">Ver más</a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <nav aria-label="Page navigation example ">
      <ul class="pagination m-0 pb-4 pt-3  justify-content-center">

        <div
          v-for="p in newPages"
          :key="p"          
        >
          <li class="page-item ">
            <router-link :to="{name:'Currencies', params: {pagina: p}}">
            <a href="" class="page-link pag-b bg-dark" @click="cambiarPagina(p)" >{{ p }}</a>
            </router-link>
          </li>
        </div>

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
    pages: []
  }),
  methods: {
    cambiarPagina(p) {      
      this.page = p;      
      axios
        .get(
          `https://api.nomics.com/v1/currencies/ticker?key=1a2b63f7fe249f264cf860de3e9ff912838c5f1b&interval=1d,30d&per-page=20&page=${this.page}`
        )
        .then((response) => {
          this.cryptos = response.data;
        })
        .catch((e) => {
          console.log(e);
        });
      window.scrollTo(0, 0);
    },
  },
  computed: {
    newPages() {
      let temp = []
      for (let i = 4; i > 0; i--) {
        if(parseInt(this.page)-i>=1) {
          temp.push(parseInt(this.page)-i)
        }        
      }
      for(let i=0;i<5;i++) {
        temp.push(i+parseInt(this.page))
      }
      return temp
    }
  },
  created() {
    this.page = this.$route.params.pagina;
    this.cambiarPagina(this.page);
  },
  
};
</script>

<style >
  .pag-b {
    border: 1px solid #3c4d6b !important;
    color: #bdc9c9;
    background-color: #2b3546 !important;
  }
  .pag-b:hover {
    color: #15b396;    
  }
  .custom-btn {
    background-color: #15b396;
    border: 1px solid rgb(54, 69, 95) !important;
  }
  .custom-btn:hover {
    background-color: rgb(4, 138, 113);
    border: 1px solid rgb(54, 69, 95) !important;
  }
  .custom-btn:active {
    background-color: rgb(1, 88, 72) !important;
    border: 1px solid rgb(54, 69, 95) !important;
  }

  .custom-dark {
    background-color: rgb(50, 54, 75);
    border: 0;
    

    
  }
</style>
