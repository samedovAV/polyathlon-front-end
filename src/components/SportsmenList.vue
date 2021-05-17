<template>
    <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Name
          </th>
          <th class="text-left">
            Calories
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="sportsman in sportsmen"
          :key="sportsman.firstName"
        >
          <td>{{ sportsman.firstName }}</td>
          <td>{{ sportsman.firstName }}</td>
          <td><router-link :to="{name: 'sportsman-details', 
                        params: {sportsman: sportsman, id: sportsman.id }}" target="_blank">
        <v-btn 
        color="orange"
        text
      >
        Explore
      </v-btn>
      </router-link></td>          
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
import http from "../http-common"; 

export default {
    name: "sportsmen-list",
    data() {
        return {
            sportsmen: []
        };
    },
    methods: {
        retrieveSportsmen() {
            http
                .get("/sportsman/list")
                .then(response => {
                    this.sportsmen = response.data;
                })
        },
        refreshList() {
            this.retrieveSportsmen();
        }
    },
    mounted() {
        this.retrieveSportsmen();
    }
}
</script>