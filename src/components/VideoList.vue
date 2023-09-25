<template>
  <ul class="list-group col-md-4">
    <!-- 
      v-for="oneElement in manyElements"
      :video="oneElement" 
    -->
    <!-- :key is needed because it enhances the performance of re-rendering our list of items-->
    <VideoListItem
      v-for="video in videos"
      :video="video"
      :key="video.etag"
      @videoSelect="onVideoSelect"
    ></VideoListItem>
  </ul>
</template>

<script>
import VideoListItem from "./VideoListItem";

export default {
  name: "VideoList",
  components: {
    VideoListItem,
  },
  //   props: ["nameToBeUSedInsideTheChild"], OR
  //   props: {
  //     nameToBeUSedInsideTheChild: typeOfData,
  //   },
  props: {
    videos: Array,
  },
  methods: {
    onVideoSelect(video) {
      this.$emit("videoSelect", video);
    },
  },
};
</script>

<style></style>
