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
    <hr>
    <v-expansion-panels class="mb-6">
      <v-expansion-panel disable-icon-rotate>
        <v-expansion-panel-header>
          Участия в мероприятиях
        </v-expansion-panel-header>
        <v-expansion-panel-content v-for="(item,i) in participationList" :key="i" ripple >
          {{item.name}}
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
        sportsman: {},
        participationList: []
    }
  },
  methods: {
       getSportsman() {
           http
            .get('sportsman/list/' + this.$route.params.id)
            .then(response => {
                this.sportsman = response.data;
            })
       },
       getParticipationList() {
         http
          .get('participation/list?sportsmanId' + this.$route.params.id)
          .then(response => {
            this.participationList = response.data;
          })
       }
   },
  mounted() {
      this.getSportsman(),
      this.getParticipationList()
  }   
  // call via API event
};
</script>

<style>
</style>