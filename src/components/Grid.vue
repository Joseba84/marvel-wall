<template>
  <article>
     <a v-for="item in characters" href="" class="card fl w-50 w-25-l link overflow-hidden">
       <div class="wrapper">
        <p>{{ item.name }}</p>
       </div>  
      <div role="img" aria-label="" class="grow aspect-ratio--4x6 " :style="{ 'background-image': 'url(' + item.thumbnail.path  + '.'+item.thumbnail.extension + ')'}"></div>
    </a>
  </article>
   
</template>

<script>
import axios from 'axios';
import cryptojs from 'crypto-js';

const apiconfig = require('../../config/api-config.js');

export default {
  name: 'grid',
  mounted() {
    this.getData();
  },
  data() {
    return {
      characters: [],
    };
  },
  methods: {
    getData() {
      const ts = apiconfig.TS;
      const pkey = apiconfig.PKEY;
      const hash = apiconfig.HASH;
      const concatToHash = cryptojs.MD5(`${ts}${hash}${pkey}`).toString();
      const limit = 50;

      axios.get(`https://gateway.marvel.com/v1/public/characters?limit=${limit}&ts=${ts}&apikey=${pkey}&hash=${concatToHash}`)
      .then((response) => {
        this.characters = response.data.data.results;
      })
      .catch((error) => {
        console.log(error);
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
