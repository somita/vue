<template lang="pug">
  <div id="app">
    <img src="./assets/logo.png">
    h1 Album Music
    select(v-model="selectedCountry")
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name}}
    spinner(v-show="loading")
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid") 
    
  </div>
</template>
<script>
import Artist from './components/Artist.vue'

import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists:[],
      countries:[
      { name:'Mexico',value:'mexico'},
      { name:'Argentina',value:'argentina'},
      { name:'Alemania',value:'germany'},
      { name:'España',value:'spain'},
      ],
      selectedCountry: 'mexico'
      
    }
  },
  components:{
    Artist
  },
  methods:{
    refreshArtists(){
      const self = this
    getArtists(this.selectedCountry)
      .then(function (artists) {
        self.artists = artists
      })

    }
  },
  mounted(){
    this.refreshArtists()
  },
  watch: {
    selectedCountry(){
      this.refreshArtists()

    }
  }
}
</script>

<style>
.loader,
.loader:after {
  border-radius: 50%;
  width: 10em;
  height: 10em;
}
.loader {
  margin: 60px auto;
  font-size: 10px;
  position: relative;
  text-indent: -9999em;
  border-top: 1.1em solid rgba(15,111,140, 0.2);
  border-right: 1.1em solid rgba(15,111,140, 0.2);
  border-bottom: 1.1em solid rgba(15,111,140, 0.2);
  border-left: 1.1em solid #0f6f8c;
  -webkit-transform: translateZ(0);
  -ms-transform: translateZ(0);
  transform: translateZ(0);
  -webkit-animation: load8 1.1s infinite linear;
  animation: load8 1.1s infinite linear;
}
@-webkit-keyframes load8 {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
@keyframes load8 {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}

</style>