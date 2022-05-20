<template>
      <Header />
      <div class="container">
            <router-view />
      </div>
</template>

<script>
import Header from "@/components/Header.vue";

export default {
      components: {
            Header,
      },
};
</script>

<style>
* {
      margin: 0;
      padding: 0;
      outline: none;
      text-decoration: none;
      list-style-type: none;
      box-sizing: border-box;
      text-transform: capitalize !important;
}
</style>
