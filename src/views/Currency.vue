<template>
  <div class="currencies">
    <div v-if="isLoading">
      <div class="loading">
        <div class="h-100 row align-items-center justify-content-center">
          <div class="text-center d-block">
            <div
              class="spinner-border loading-color"
              style="width: 3rem; height: 3rem"
              role="status"
            >
              <span class="visually-hidden"></span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="container pb-4">
      <div class="d-flex align-items-center justify-content-center">
        <div class="text-center">
          <div class="row text-white text-center">
            <p class="pr-3">USD</p>
            <label class="switch">
              <input type="checkbox" v-model="checked" />
              <span class="slider round" @click="cambiarMoneda(page)"></span>
            </label>
            <p class="pl-3">MXN</p>
          </div>
        </div>
      </div>
    </div>

    <div class="row d-flex justify-content-center">
      <div class="" v-for="c in cryptos" :key="c.id">
        <div class="col-3">
          <div
            class="card text-white custom-dark mb-4"
            style="width: 18rem; z-index: 10"
          >
            <img
              class="card-img-top p-5"
              :src="c.logo_url"
              :alt="'Logo ' + c.id"
              style="height: 18rem; max-width: 18rem"
            />
            <div class="card-body">
              <h5 class="card-title">{{ c.name }}</h5>
              <p class="card-text">
                $ <strong>{{ c.price }}</strong> {{ convert }}
              </p>
              <p class="card-text">
                <span class="badge rounded-pill bg-tag">{{
                  c.price_date
                }}</span>
              </p>
              <a class="btn custom-btn btn-primary w-100">Details</a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <nav aria-label="Page navigation example ">
      <ul class="pagination m-0 pb-5 pt-4 justify-content-center">
        <li class="page-item">
          <router-link :to="{ name: 'Currencies', params: { pagina: 1 } }">
            <a
              href=""
              class="page-link pag-b bg-dark"
              @click="cambiarPagina(1)"
              >{{ simbols[0] }}</a
            >
          </router-link>
        </li>

        <div v-for="p in newPages" :key="p">
          <li class="page-item">
            <router-link :to="{ name: 'Currencies', params: { pagina: p } }">
              <a
                href=""
                class="page-link pag-b bg-dark"
                @click="cambiarPagina(p)"
                >{{ p }}</a
              >
            </router-link>
          </li>
        </div>

        <li class="page-item">
          <router-link :to="{ name: 'Currencies', params: { pagina: 99 } }">
            <a
              href=""
              class="page-link pag-b bg-dark"
              @click="cambiarPagina(99)"
              >{{ simbols[1] }}</a
            >
          </router-link>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Currency",
  data: () => ({
    cryptos: [],
    page: 1,
    pages: [],
    simbols: ["<<", ">>"],
    isLoading: false,
    checked: false,
    convert: 'MXN',
  }),
  methods: {
    cambiarPagina(p) {
      this.page = p;
      window.scrollTo(0, 0);
      this.isLoading = true;
      const url = `https://api.nomics.com/v1/currencies/ticker?key=1a2b63f7fe249f264cf860de3e9ff912838c5f1b&interval=1d,30d&per-page=20&page=${this.page}&convert=${this.convert}`;
      axios
        .get(url)
        .then((response) => {
          this.cryptos = response.data;
        })
        .catch((e) => {
          console.log(e);
        })
        .finally(() => {
          this.isLoading = false;
        });
    },
	cambiarMoneda(p) {
      if (this.checked) {
        this.convert = "USD";
      } else {
        this.convert = "MXN";
      }
		this.cambiarPagina(p)
	}
  },
  computed: {
    newPages() {
      let temp = [];
      for (let i = 4; i > 0; i--) {
        if (parseInt(this.page) - i >= 1) {
          temp.push(parseInt(this.page) - i);
        }
      }
      for (let i = 0; i < 5; i++) {
        if (i + parseInt(this.page) > 0 && i + parseInt(this.page) < 100) {
          temp.push(i + parseInt(this.page));
        }
      }
      return temp;
    },
    // convert() {
    // 	return this.checked ? 'USD' : 'MXN'
    // },
  },
  created() {
    this.page = this.$route.params.pagina;
    this.cambiarPagina(this.page);
  },
  beforeMount() {
    this.checked = true;
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
.loading-color {
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
  box-shadow: 4px 4px 4px #2c2d3d;
}

.bg-tag {
  background-color: #395e9e;
}

.loading {
  position: fixed;
  width: 100vw;
  height: 100vh;
  left: 0;
  top: 0;
  background: rgba(82, 101, 163, 0.7);
  z-index: 10000 !important;
}

.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #1f2a3b;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}
.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}
input:checked + .slider {
  background-color: #15b396;
}
input:focus + .slider {
  box-shadow: 0 0 1px #15b396;
}
input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}
.slider.round {
  border-radius: 34px;
}
.slider.round:before {
  border-radius: 50%;
}
</style>