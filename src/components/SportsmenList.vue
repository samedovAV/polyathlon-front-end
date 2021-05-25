<template>
<v-app>
    <v-data-table
      :headers="headers"
      :items="sportsmen"
      class="elevation-1"
    >
    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>Глобальный список участников</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <div data-app>
          <add-sportsmen-form-modal/>
        </div>
      </v-toolbar>
    </template>
    <template v-slot:[`item.action`]="{ item }">
      <router-link :to="{name: 'sportsman-details', 
                        params: { id: item.id }}" target="_blank">
      <v-icon
        small
        class="mr-2"
      >
        mdi-open-in-new
      </v-icon>
      </router-link>
      <v-icon
        small
        class="mr-2"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        class="mr-2"
        v-on:click="() => deleteSportsman(item.id)"
        @click="reloadPage"
      >
        mdi-delete
      </v-icon>
    </template>
  </v-data-table>
  <router-view @refreshData="refreshList"></router-view>
</v-app>
</template>

<script>
import http from "../http-common";
import AddSportsmenFormModal from "./AddSportsmenFormModal.vue"; 

export default {
    name: "sportsmen-list",
    components: {
      AddSportsmenFormModal
    },
    data() {
        return {
            sportsmen: [],
            headers: [
              {
                text: 'Имя',
                align: 'start',
                sortable: false,
                value: 'firstName',
              },
              { text: 'Фамилия', value: 'lastName' },
              { text: 'Год рождения', value: 'yearOfBirth'},
              { text: "Действия", value: "action" }
          ]
        };
    },
    methods: {
        async retrieveSportsmen() {

          const sportsmenRes = (await http.get("/sportsman/list")).data

          this.sportsmen = sportsmenRes
        },
        refreshList() {
            this.retrieveSportsmen();
        },
        async deleteSportsman(id) {
          await http.delete("/sportsman/list/" + id)
          .then(() => {this.$emit("refreshData")})
        },
        reloadPage() {
          window.location.reload();
        } 
    },
    mounted() {
        this.retrieveSportsmen();
        this.refreshList()
    }
}
</script>