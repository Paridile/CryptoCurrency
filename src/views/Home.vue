<template>
  <div class="currencies">    
    <Currencies/>
    
  </div>
</template>

<script>
// @ is an alias to /src

import Currencies from '../components/Currencies.vue';

export default {
  name: "Home",
  components: {
    Currencies
  },
};
</script>
