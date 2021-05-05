<template>
    <div id="app" class="container-fluid">
        <app-header />
        <br/>
        <router-view/>
        <app-footer />
    </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";

export default {
  name: "app",
  components: {
    AppHeader,
    AppFooter
  }
};
</script>

<style>
.site-info {
  color: blue;
  margin-bottom: 20px;
}

.btn-primary {
  margin-right: 5px;
}

.container-fluid {
  text-align: center;
}
</style>
