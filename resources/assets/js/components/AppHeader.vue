<template>
  <div >
<nav class="navbar" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <a class="navbar-item" href="https://bulma.io">
      PhoneBook
    </a>

    <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false">
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
  </div>

  <div class="navbar-menu">
    <router-link class="button is-default" to="/">Home</router-link>
    <router-link class="button is-default" to="/about">About</router-link>
  </div>

</nav>
  </div>
</template>
<script>
export default {
  name: "app-header"
};
</script>
