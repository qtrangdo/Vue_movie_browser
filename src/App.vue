<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoDetail :video="selectedVideo"/>
    <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList> 
  </div>
</template>

<script>
  import axios from 'axios';
  import SearchBar from './components/SearchBar';
  import VideoList from './components/VideoList';
  import VideoDetail from './components/VideoDetail';
  import {API_KEY} from './config.js';

  export default {
    name: "App",
    components: {
      SearchBar,
      VideoList,
      VideoDetail,
    },
    data() {
      return { videos: [], selectedVideo: null }
    },
    methods: {
      onVideoSelect(video) {
        this.selectedVideo = video;
      },
      onTermChange(searchTerm) {
        axios.get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm,
          }
        })
          .then(res => {
            this.videos = res.data.items;
          })
      }
    }
  };
</script>