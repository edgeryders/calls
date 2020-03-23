<template>
    <div class="content_wrapper md:content_wrapper-md">
      <div class="hero_image md:hero_image-md" v-if="data.image.url" :style="{flexBasis: data.image.width + 'px'}">
        <img :src="getAsset(data.image.url)" />
      </div>
      <div class="md:pt-1">
        <h1 class="hero_title md:hero_title-md">{{ data.title }}</h1>
        <div class="hero_text" v-html="data.text.content" :style="{textAlign: data.text.align}"></div>
        <div class="action_container">
          <a class="action" v-for="item in data.text.buttons" :style="styleObj(item)" :href="item.url" :key="item.url" target="_blank">
            {{item.text}}
          </a>
        </div>
      </div>

      <div class="hero_video" v-if="data.background.video">
        <video autoplay loop muted>
          <source :src="data.background.video" type="video/mp4">
        </video>
      </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  filters: {
    formatDate: function(value) {
      return moment(String(value)).format("MMMM Do YYYY");
    }
  },
  methods: {
    styleObj(item) {
      var styleObj = {
        background: '#000',
        color: '#fff'
      };
      if (item.background) {
        styleObj["background"] = item.background;
      };
      if (item.color) {
        styleObj["color"] = item.color;
      };
      return styleObj;
    },
     getAsset(file) {
      return require("@/assets/" + file);
    }
  },
  props: ["data"]
};
</script>
