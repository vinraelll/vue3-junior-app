<template>
  <nav class="teal lighten-2">
    <div class="nav-wrapper container-lg">
      <router-link to="/" class="brand-logo">Tasks</router-link>
      <ul id="nav-mobile" class="right hide-on-med-and-down">
        <li>
          <router-link
            to="/"
            exact
            active-class="active"
          >
            Create
          </router-link>
        </li>
        <li>
          <router-link
            to="/list"
            exact
            active-class="active"
          >
            List
          </router-link>
        </li>
        <li>
          <router-link
            to="/task/:id"
            exact
            active-class="active"
          >
            Task
          </router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar'
}
</script>

<style scoped>
nav {
  padding: 0 2rem;
}

.active {
  background-color: #0000001a;
}
</style>