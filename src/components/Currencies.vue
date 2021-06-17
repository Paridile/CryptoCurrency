<template>
  <div class="currencies">
    <div class="row">
      <div class="" v-for="c in cryptos" :key="c.id">
        <div class="col-12">
          <b-card
            :title="c.id"
            :img-src="c.logo_url"
            img-alt="Image"
            img-top
            tag="article"
            class="mb-2"
          >
            <b-card-text>
              Some quick example text to build on the card title and make up the
              bulk of the card's content.
            </b-card-text>

            <b-button href="#" variant="primary">Go somewhere</b-button>
          </b-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Currencies",
  data: () => ({
    cryptos: [],
    errors: [],
  }),
  created() {
    axios
      .get(
        "https://api.nomics.com/v1/currencies/ticker?key=1a2b63f7fe249f264cf860de3e9ff912838c5f1b&interval=1d,30d&per-page=20&page=1"
      )
      .then((response) => {
        this.cryptos = response.data;
      })
      .catch((e) => {
        console.log(e);
      });
  },

  props: {},
};
</script>

<style scoped>
</style>
