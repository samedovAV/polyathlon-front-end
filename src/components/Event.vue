<template>
  <!--<div>Profile No.{{ $route.params.id }}</div>-->
  <v-card>
    <v-img
      src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
      height="200px"
    ></v-img>

    <v-card-title>
      {{event.description}}
    </v-card-title>

    <v-card-subtitle>
      1,000 miles of wonder
    </v-card-subtitle>

    <v-card-actions>
      <v-btn
        color="orange lighten-2"
        text
      >
        Explore
      </v-btn>

    </v-card-actions>


  </v-card>
</template>

<script>
import http from "../http-common";

export default {
  name: "event",
  data() {
    return {
      event: {}
    }
  },
  methods: {
    getEvent() {
      http
      .get('events/list/' + this.$route.params.id)
      .then(response => {
        this.event = response.data;
      })
    }
  },
  mounted() {
    this.getEvent()
  }
  // call via API event
};
</script>

<style>
</style>
