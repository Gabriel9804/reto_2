<template lang="html">
  <div :class="['podcast',{
      'podcast--active': active,
  }]">
    <img class="podcast_image" :src="image" :alt="name" />
    <p class="podcast_name">{{ name }}</p>
  </div>
</template>

<script>
export default {
  name: "FuPodcast",
  props: {
    image: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    active:{
        type: Boolean,
        default: false,
        required: false,
    }
  },
};
</script>

<style lang="css" scoped>
.podcast {
  width: 145px;
  text-align: center;
  cursor: pointer;
}
.podcast--active{
    border: 5px solid #2196F3;
}
.podcast_image {
  width: 144px;
  height: 164px;
  object-fit: cover;
}
.podcast_name {
  margin: 0;
  font-size: 14px;
  font-weight: bold;
  margin-top: 4px;
}
</style>
