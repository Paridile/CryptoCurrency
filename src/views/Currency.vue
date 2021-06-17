<template>
  <div class="currencies background-dark">    
	  <div class="text-center">
		  <h1 class="display-2 text-white">
			  Crypto currencies
		  </h1>
	  </div>
    <Currencies />
    
  </div>
</template>

<script>
// @ is an alias to /src

import Currencies from '../components/Currencies.vue';

export default {
  name: "Currencies",
  components: {
    Currencies
  },
};
</script>


