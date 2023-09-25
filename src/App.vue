<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoDetail :video="selectedVideo"></VideoDetail>
    <!-- v-bind:smth="smth"  ===  :smth="smth" -->
    <!-- v-bind:nameToBeUSedInsideTheChild="propertyNameInDataOfParent" -->
    <VideoList :videos="videos" @videoSelect="onVideoSelect"></VideoList>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";

// this is basically te same as writing inside of 'new Vue'
export default {
  name: "App",
  // data: {},
  // computed: {},
  // methods: {},

  // This lets Vue know that it should expect to find a SeacrhBar component in the template
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },
  // This is a component, so data needs to be a function that returns an object. Data can simply be an object only in vue instances
  data() {
    return {
      videos: [],
      selectedVideo: null,
    };
  },
  methods: {
    // onTermChange: function() {} = onTermChange() {}
    onTermChange(seacrhTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: process.env.VUE_APP_API_KEY,
            type: "video",
            part: "snippet",
            q: seacrhTerm,
          },
        })
        .then((response) => {
          this.videos = response.data.items;
          console.log(response);
        });
    },
    onVideoSelect(video) {
      this.selectedVideo = video;
    },
  },
};
</script>
