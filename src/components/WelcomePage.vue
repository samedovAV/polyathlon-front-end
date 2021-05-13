<template>
  <div style="margin-top: 30vh" fill-height align="center"
      justify="center">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li>
        <router-link to="/home" class="nav-link">
          <v-btn rounded color="primary" dark>Home</v-btn>
        </router-link>
      </li>
      <li>
        <router-link to="/customers" class="nav-link">
          <v-btn rounded color="primary" dark>Customers (test)</v-btn>
        </router-link>
      </li>
      <li>
        <router-link to="/events" class="nav-link">
          <v-btn rounded color="primary" dark>Events</v-btn>
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'WelcomePage',
  data() {
    return {
      msg: 'Welcome to Polyathlon App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.hello {
  margin-top: 25%;
}
</style>