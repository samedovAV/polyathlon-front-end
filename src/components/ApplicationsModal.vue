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
          Просмотреть заявки
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="headline grey lighten-2">
          Privacy Policy
        </v-card-title>

        <v-card-text>
            <v-simple-table>
            <template v-slot:default>
              <thead>
                <tr>
                  <th class="text-left">
                    Университет
                  </th>
                  <th class="text-left">
                    Представитель
                  </th>
                  <th class="text-left">
                    Действия
                  </th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="item in event.applicationList"
                  :key="item.name"
                >
                  <td>{{ item.university }}</td>
                  <td>{{ item.creator.username }}</td>
                  <td><v-btn
                        rounded
                        color="primary"
                        dark
                        v-on:click="saveApplication"
                      >
                        Принять заявку
                      </v-btn>
                  </td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="dialog = false"
          >
            I accept
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
  export default {
    props: ['event'],
    data () {
      return {
        dialog: false,
      }
    },
  }
</script>