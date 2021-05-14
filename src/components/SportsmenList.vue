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
          v-for="item in sportsmen"
          :key="item.firstName"
        >
          <td>{{ item.firstName }}</td>
          <td>{{ item.firstName }}</td>
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