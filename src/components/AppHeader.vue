<template>
<div>
    <v-app-bar
      color="deep-purple accent-4"
      dense
      dark
    >
      
      <v-btn>
        <router-link to="/" class="nav-link">
            <font-awesome-icon icon="home" /> Home
        </router-link>
      </v-btn>

      <v-toolbar-title>Page title</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn v-if="showAdminBoard">
        <router-link to="/calendar" class="nav-link" target="_blank">Calendar</router-link>
      </v-btn>

      <v-btn v-if="showAdminBoard">
        <router-link to="/admin" class="nav-link">Admin Board</router-link>
      </v-btn>

      <v-btn v-if="showModeratorBoard">
        <router-link to="/mod" class="nav-link">Moderator Board</router-link>
      </v-btn>
      <!--
      <v-btn v-if="currentUser">
        <router-link v-if="currentUser" to="/user" class="nav-link">User</router-link>
      </v-btn>-->

      <v-btn v-if="!currentUser">
        <router-link to="/register" class="nav-link">
          <font-awesome-icon icon="user-plus" />Sign Up
        </router-link>
      </v-btn>

      <v-btn v-if="!currentUser">
        <router-link to="/login" class="nav-link">
            <font-awesome-icon icon="sign-in-alt" />Login
        </router-link>
      </v-btn>

      <v-btn v-if="currentUser">
        <router-link to="/profile" class="nav-link">
            <font-awesome-icon icon="user" />
            {{ currentUser.username }}
          </router-link>
      </v-btn>

      <v-btn v-if="currentUser">
        <a class="nav-link" href @click.prevent="logOut">
          <font-awesome-icon icon="sign-out-alt" />LogOut
        </a>
      </v-btn>
      
    </v-app-bar>

    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    currentUser() {
      return this.$store.state.auth.user;
    },
    showAdminBoard() {
      if (this.currentUser && this.currentUser.roles) {
        return this.currentUser.roles.includes('ROLE_ADMIN');
      }

      return false;
    },
    showModeratorBoard() {
      if (this.currentUser && this.currentUser.roles) {
        return this.currentUser.roles.includes('ROLE_MODERATOR');
      }

      return false;
    }
  },
  methods: {
    logOut() {
      this.$store.dispatch('auth/logout');
      this.$router.push('/');
    }
  }
}
</script>

<style >  
</style>