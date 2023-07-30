<template></template>
<script setup>
import nuxtStorage from "nuxt-storage";
const router = useRouter();

onMounted(() => {
  nuxtStorage.localStorage.setData("user", null);
  router.push({ path: "/login" });
});
</script>
