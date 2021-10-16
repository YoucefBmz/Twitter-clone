<template>
  <div id="nav" class="text-center bg-blue text-2xl py-5">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>

  <router-view/>
</template>

<script>
export default {
    name: 'navBar'
}
</script>

<style>

</style>