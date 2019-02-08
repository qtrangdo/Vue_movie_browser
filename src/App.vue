<template>
  <div>
    <SearchBar @termChange="onTermChange"></SearchBar>
  </div>
</template>

<script>
  import axios from 'axios';
  import SearchBar from './components/SearchBar';
  import API_KEY from './config.js';
  const key = API_KEY;
  export default {
    name: "App",
    components: {
      SearchBar
    },
    methods: {
      onTermChange(searchTerm) {
        axios.get('https://googleapis.com/youtube/v3/search', {
          params: {
            key,
            type: 'video',
            part: 'snippet',
            q: searchTerm,
          }
        })
          .then( res => console.log(res))
      }
    }
  };
</script>