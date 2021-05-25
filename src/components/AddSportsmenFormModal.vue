<template>
  <div class="text-left">
    <v-dialog
      v-model="dialog"
      width="500"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="red lighten-2"
          dark
          v-bind="attrs"
          v-on="on"
        >
          Добавить участника
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="headline grey lighten-2">
          Добавить участника
        </v-card-title>

        <v-card-text>
            <v-form>
            <v-container>
            <v-row>
                <v-col
                cols="12"
                md="4"
                >
                <v-text-field
                    v-model="sportsman.firstName"
                    :counter="10"
                    label="Имя"
                    required
                ></v-text-field>
                </v-col>

                <v-col
                cols="12"
                md="4"
                >
                <v-text-field
                    v-model="sportsman.lastName"
                    :counter="10"
                    label="Фамилия"
                    required
                ></v-text-field>
                </v-col>

                <v-col
                cols="12"
                md="4"
                >
                <v-text-field
                    v-model="sportsman.yearOfBirth"
                    label="Год рождения"
                    required
                ></v-text-field>
                </v-col>
            </v-row>
            </v-container>
            </v-form>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            v-on:click="saveSportsman"
            @click="reloadPage"
          >
            Добавить
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <router-view @refreshData="refreshList"></router-view>
  </div>
</template>

<script>
import http from "../http-common";

  export default {
    data () {
      return {
        dialog: false,
        sportsman: {},
        submitted: false
      }
    },
    methods: {
        saveSportsman() {
            var data = {
                firstName: this.sportsman.firstName,
                lastName: this.sportsman.lastName,
                yearOfBirth: this.sportsman.yearOfBirth
            }

            http
                .post("/sportsman/add-sportsman", data)
                .then(response => {
                    this.sportsman.id = response.data.id
                    this.$emit("refreshData");
                })
            this.submitted = true
            this.dialog = false
        },
        reloadPage() {
          window.location.reload();
        } 
    }
  }
</script>