<template>
  <v-form>
    <v-container v-if="!submitted">
      <v-row>
        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
            v-model="partApplication.university"
            :counter="10"
            label="University"
            required
          ></v-text-field>
          <v-text-field
            v-model="currentUser.username"
            :counter="10"
            required
          ></v-text-field>
        </v-col>
      </v-row>
      <v-btn
        rounded
        color="primary"
        dark
        v-on:click="saveApplication"
      >
        Отправить
      </v-btn>
    </v-container>
    <div v-else>
      <h4>You submitted successfully!</h4>
      <button class="btn btn-success" v-on:click="newPartApplication">Add</button>
    </div>
  </v-form>
</template>

<script>
import http from "../http-common";

  export default {
    name: "add-participation-application",
    computed: {
      currentUser() {
        return this.$store.state.auth.user;
      } 
    },
    data() {
      return {
        partApplication: {
          eventId: this.$route.params.id,
          university: '',
          creator: {},
          sportsmen: []
        },
        submitted: false
      }
    },
    methods: {
      saveApplication() {
        var data = {
          id: this.$route.params.id,
          university: this.partApplication.university,
          creator: this.currentUser
        }

        http
          .post("/part-application/send-application", data)
          .then(response => {
            this.partApplication.id = response.data.id
            this.partApplication.creator = response.data.creator
          })
        this.submitted = true  
      },
      newPartApplication() {
        this.submitted = false
        this.partApplication = {}
      }
    }
    /*
    data: () => ({
      valid: false,
      firstname: '',
      lastname: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
    }),
    */
  }
</script>