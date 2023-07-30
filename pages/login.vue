<template>
  <div class="container">
    <form id="loginform" class="form">
      <h2 style="text-align: center">Giriş Yap</h2>
      <fieldset>
        <legend>
          <input type="text" v-model="username" placeholder="kullanıcı adı" />
          <input type="password" v-model="password" placeholder="şifre" />
          <button @click="login" class="btn">Login</button>
        </legend>
      </fieldset>
    </form>
  </div>
</template>
<script setup>
const username = ref("");
const password = ref("");
const router = useRouter();
const a = useState("qwe", () => 0);

import nuxtStorage from "nuxt-storage";

function login(e) {
  e.preventDefault();
  if (username.value == "test" && password.value == "1234") {
    nuxtStorage.localStorage.setData(
      "user",
      username.value + password.value,
      "1h"
    );
    router.push({ path: "/" });
  } else {
    alert("Wrong Password ");
  }
}
</script>
