<template>
  <div class="container" style="flex-direction: column">
    <label for="">Title</label>
    <input type="text" v-model="title" />
    <br />
    <label for="">aciliyet: </label>
    <select v-model="selected">
      <option disabled value="">Please select one</option>
      <option>A</option>
      <option>B</option>
      <option>C</option>
    </select>
    <br />
    <label for="">Açıklama</label>
    <input type="text" v-model="explanation" />
    <button @click="handleSubmit">Send</button>
  </div>
</template>
<script setup>
const selected = ref(null);
const explanation = ref(null);
const title = ref(null);

import nuxtStorage from "nuxt-storage";

function handleSubmit(e) {
  e.preventDefault();
  console.log(selected.value, explanation.value);

  let callsData = nuxtStorage.localStorage.getData("calls");
  if (!callsData) {
    nuxtStorage.localStorage.setData(
      "calls",
      JSON.stringify({ calls: [] }),
      "1h"
    );
  }

  function makeid(length) {
    let result = "";
    const characters =
      "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
    const charactersLength = characters.length;
    let counter = 0;
    while (counter < length) {
      result += characters.charAt(Math.floor(Math.random() * charactersLength));
      counter += 1;
    }
    return result;
  }

  let calls = JSON.parse(callsData);
  let newCall = {
    title: title.value,
    selected: selected.value,
    explanation: explanation.value,
    date: new Date(Date.now()).toLocaleDateString("tr-TR"),
    user: nuxtStorage.localStorage.getData("user") || "undefinedUser",
    id: makeid(5),
  };

  calls.calls.push(newCall);

  let jsonData = JSON.stringify(calls);

  nuxtStorage.localStorage.setData("calls", jsonData);
  alert("done.");
}
</script>
