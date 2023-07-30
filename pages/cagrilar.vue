<template>
  <div>cagrilar</div>
  <ul class="call-list">
    <div
      style="cursor: pointer"
      @click="gotoUpdate(call.id)"
      v-for="call in calls"
      :key="call.title"
    >
      <div
        class="callBox"
        :style="{ backgroundColor: call.selected == 'C' ? 'red' : '' }"
      >
        <h1>{{ call.title }}</h1>
        <hr />
        <p>aciklama: {{ call.explanation }}</p>
        <p>tarih: {{ call.date }}</p>
        <p>birim: {{ call.user }}</p>
        <p>ID: {{ call.id }}</p>
      </div>
    </div>
  </ul>
</template>
<script setup>
import nuxtStorage from "nuxt-storage";
const router = useRouter();
let calls = ref(null);
onMounted(() => {
  let callsData = nuxtStorage.localStorage.getData("calls");

  let calls1 = JSON.parse(callsData);
  calls.value = calls1?.calls;
});
function gotoUpdate(id) {
  router.push({ path: `/updatecall/${id}` });
}
</script>
<style>
.callBox {
  border: 1px solid black;
  padding: 20px 100px;
  box-sizing: border-box;
}
.call-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
  justify-content: center;
  align-items: center;
  padding: 10px 300px;
}
</style>
