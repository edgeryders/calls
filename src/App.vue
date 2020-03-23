<template>
  <div class="flex flex-col w-full">
    <Nav style="margin-bottom: 60px" :data="getNavElements" />

    <Hero :baseUrl="data.baseUrl" :custom="getSectionData('hero')"/>

    <div v-for="section in sections" :key="section.title" :id="section.id">
      <Custom v-if="section.type == 'custom'" :custom="section" html=true />
      <Events v-if="section.type == 'events'" :baseUrl="data.baseUrl" :custom="section" />
    </div>

    <Terms />
  </div>
</template>

<script>
import data from "@/data/config.json";
import axios from "axios";

import Nav from "@/components/Navigation.vue";
import Hero from "@/components/Hero.vue";
import Custom from "@/components/Custom.vue";
import Events from "@/components/Events.vue";
import Terms from "@/components/Terms.vue";

export default {
  name: "home",
  data() {
    return {
      data,
      category: { users: [] },
      categories: [],
      sections: null
    };
  },
  components: {
    Events,
    Hero,
    Nav,
    Custom,
    Terms
  },
  created() {
    if (this.data.configId) {
      axios.get(
        `https://edgeryders.eu/webkit_components/topics.json?serializer=event&tags=webcontent`
      ).then(({ data }) => {
        var post = data.find(post => post.id === this.data.configId);
        var json = this.getJson(post.cooked);
        this.sections = json.sections;
      });
    } else {
      this.sections = this.data.sections;
    }
  },
  methods: {
    getSectionData(type) {
      return this.sections.find(section => section.type === type) || {};
    },
    getNavElements() {
      if (this.sections.length) {
      var navArray = this.sections.map(function(el) {
            if (el.id) {
              return {
                title: el.title,
                id: el.id,
              } 
            }
          });
      return navArray.filter(function (el) {
          return el != null;
      });
      }
    }
  },
  computed: {
  }
};
</script>
