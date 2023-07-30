<template>
  <menu>
    <NuxtLink to="/"><img class="logo" src="logo.svg" alt="logo" /></NuxtLink>
    <NuxtLink to="/cagrilar" onclick="route()">Devam eden çağrılar</NuxtLink>
    <NuxtLink to="/yenicagri" onclick="route()">Yeni çağrı</NuxtLink>
    <NuxtLink to="/logout" onclick="route()">Çıkış yap</NuxtLink>
  </menu>
  <div>
    <NuxtPage />
  </div>
</template>
