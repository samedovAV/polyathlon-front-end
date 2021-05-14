<template>
    <v-card
    class="mx-auto"
    >
        <v-list></v-list>
    </v-card>
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