<template>
  <ul>
    <li v-for="(gif, index) in gifs" v-bind:key="index">
      <img :src="gif.images.fixed_height.url" />
    </li>
  </ul>
</template>

<script>
export default {
  props: ["gifs"],
}
</script>

<style>
li {
  list-style: none;
  float: left;
  margin: 20px;
}
</style>