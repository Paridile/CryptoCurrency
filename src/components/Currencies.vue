<template>
  <div class="currencies background-dark">    
    <div class="container">
	  <div class="text-center container">
		  <h1 class="display-4 pt-3 pb-5  text-white">
			  Cryptocurrencies
		  </h1>
	  </div>
    </div>
    <Currency />
    
  </div>
</template>

<script>
// @ is an alias to /src

import Currency from '../views/Currency.vue';

export default {
  name: "Currencies",
  components: {
    Currency
  },
};
</script>