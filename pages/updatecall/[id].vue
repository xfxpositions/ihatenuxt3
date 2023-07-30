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
    <label for="">id</label>
    <input type="text" v-model="idcall" />
    <button @click="handleSubmit">Send</button>
  </div>
</template>
<script setup>
import nuxtStorage from "nuxt-storage";
let title = ref("");
let date = ref("");
let idcall = ref("");
let selected = ref("");
let explanation = ref("");
let index = 0;
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
    id: idcall.value,
  };

  calls.calls[index - 1] = newCall;

  let jsonData = JSON.stringify(calls);

  nuxtStorage.localStorage.setData("calls", jsonData, "1h");
  alert("done.");
}
onMounted(() => {
  let callsData = nuxtStorage.localStorage.getData("calls");
  let calls = JSON.parse(callsData);
  let route = useRoute();
  let id = route.params.id;

  console.log(calls);
  let found = false;
  for (const ccall of calls.calls) {
    if (ccall?.id == id) {
      found = true;
      title.value = ccall.title;
      date.value = ccall.date;
      idcall.value = ccall.id;
      selected.value = ccall.seleced;
      explanation.value = ccall.explanation;
    }
    index++;
  }
  if (!found) {
    alert("found nothing. check your id dumb");
  }
});
</script>
