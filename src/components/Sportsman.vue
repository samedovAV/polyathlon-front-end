<template>
  <!--<div>Profile No.{{ $route.params.id }}</div>-->
  <v-card>
    <v-img
      src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
      height="200px"
    ></v-img>

    <v-card-title>
     {{sportsman.firstName}}
    </v-card-title>

    <v-card-subtitle>
      {{sportsman.lastName}}
    </v-card-subtitle>

    <v-card-actions>
      <v-btn
        color="orange lighten-2"
        text
      >
        Explore
      </v-btn>

      <v-spacer></v-spacer>

      <v-btn
        color="orange lighten-2"
        text
      >
        
      </v-btn>

    </v-card-actions>

     <v-expansion-panels>
    <v-expansion-panel>
      <v-expansion-panel-header>
        Список мероприятий
      </v-expansion-panel-header>
      <v-expansion-panel-content>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
      </v-expansion-panel-content>
    </v-expansion-panel>
  </v-expansion-panels>
  </v-card>
</template>

<script>
import http from "../http-common";

export default {
  name: "sportsman",
   data() {   
    return {
        sportsman: {}
    }
  },
  methods: {
       getSportsman() {
           http
            .get('sportsman/list/' + this.$route.params.id)
            .then(response => {
                this.sportsman = response.data;
            })
       }
   },
  mounted() {
      this.getSportsman()
  }   
  // call via API event
};
</script>

<style>
</style>