<template>
  <div class="hero md:hero-md">
    
    <CustomView :data="custom"></CustomView>

  </div>
</template>

<script>
import moment from "moment";
import CustomView from "@/components/views/Hero_Custom.vue";

export default {
  methods: {
  },
  components: {
    CustomView,
  },
  computed: {
  },
  filters: {
    formatDate: function(value) {
      return moment(String(value)).format("MMMM Do YYYY");
    }
  },
  props: ["category", "custom", "baseUrl"]
};
</script>
