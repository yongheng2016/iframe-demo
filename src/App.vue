<template>
  <router-view />
</template>

<script setup>
import microApp from "@micro-zoe/micro-app";

microApp.start();
defineOptions({
  name: "App",
});
</script>
<style>
body {
}
</style>
