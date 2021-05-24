<template>
<div>
    <h4>Events List</h4>
    <v-container>
    <v-row v-for="(event, index) in events" :key="index">
    <v-card
    class="mx-auto"
    >
    <v-img
      class="white--text align-end"
      height="200px"
      src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
    >
    </v-img>

    <v-card-title class="pb-0">
      {{event.title}}
    </v-card-title>

    <v-card-text align="left">
      <div class="my-4 subtitle-1">{{event.description}}</div>
    </v-card-text>

    <v-card-actions>
      <v-btn
        text
        color="green"
      >
        Share
      </v-btn>

      <router-link :to="{name: 'event-details', 
                        params: {event:event, id: event.id }}" target="_blank">
        <v-btn 
        color="orange"
        text
      >
        Explore
      </v-btn>
      </router-link>

      <v-spacer></v-spacer>

      <router-link :to="{name: 'part-application', 
                        params: {event:event, id: event.id }}" target="_blank">
        <v-btn
        color="orange lighten-2"
        text
      >
        Подать заявку
      </v-btn>
      </router-link>

    </v-card-actions>
      <div data-app>
        <applications-modal :event="event"/>
      </div>
    <v-card-actions>
     
    </v-card-actions>
    </v-card>
    </v-row>
    </v-container>
</div>
</template>

<script>
import http from "../http-common";
import ApplicationsModal from './ApplicationsModal.vue'

export default {
    name: "events-list",
    components: {
      ApplicationsModal
    },
    data() {
        return {
            events: []
        };
    },
    methods: {
    retrieveEvents() {
      http
        .get("/events/list")
        .then(response => {
          this.events = response.data; // JSON are parsed automatically.
        })
    },
    refreshList() {
      this.retrieveEvents();
    }
    /* eslint-enable no-console */
  },
  mounted() {
    this.retrieveEvents();
  }
}
</script>

<style>

</style>