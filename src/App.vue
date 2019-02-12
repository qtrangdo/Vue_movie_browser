<template>
  <div>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList></VideoList>
  </div>
</template>

<script>
  import axios from 'axios';
  import SearchBar from './components/SearchBar';
  import VideoList from './components/VideoList';
  import {API_KEY} from './config.js';

  export default {
    name: "App",
    components: {
      SearchBar,
      VideoList
    },
    methods: {
      onTermChange(searchTerm) {
        axios.get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm,
          }
        })
          .then(res => console.log(res))
      }
    }
  };
</script>