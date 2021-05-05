<template>
  <header>
    <p>Polyathlon Application</p>
    <nav>
        <router-link class="btn btn-primary" to="/">Home</router-link>
        <router-link class="btn btn-primary" to="/customers">Customers</router-link>
        <router-link class="btn btn-primary" to="/add">Add</router-link>
        <router-link class="btn btn-primary" to="/search">Search</router-link>
    </nav>
  </header>
</template>

<style >
header {
    display: flex;
    border-bottom: 1px solid #ccc;
    padding: .5rem 1rem;
}

header p {
    margin-left: 1rem;
}  

nav {
    margin-left: auto;
}  

nav ul {
    list-style: none;
}  

nav ul li {
    display: inline-flex;
    margin-left: 1rem;
}   
</style>