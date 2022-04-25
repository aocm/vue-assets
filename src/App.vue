<template>
  <h1>Hello App!</h1>
  <p>
    <!-- use the router-link component for navigation. -->
    <!-- specify the link by passing the `to` prop. -->
    <!-- `<router-link>` will render an `<a>` tag with the correct `href` attribute -->
    <router-link to="/"> Go to Home </router-link>
    <span> | </span>
    <router-link to="/hello"> Go to hello </router-link>
  </p>
  <!-- route outlet -->
  <!-- component matched by the route will render here -->
  <router-view />
</template>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
