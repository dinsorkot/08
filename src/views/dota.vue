<script setup>
import { ref, onMounted } from "vue";
const items = ref([]);
const url = ref("https://api.opendota.com/api/heroStats");
const getData = async () => {
  const response = await fetch(url.value);
  const data = await response.json();
  items.value = data;
};
onMounted(() => {
  getData();
});
</script>
<template>
  <div>
    <ul>
      <li v-for="item in items" :key="item.id">
        <img :src="'https://api.opendota.com'+item.icon" :alt="item.localized_name" />
        {{
          item.localized_name
        }}
      </li>
    </ul>
  </div>
</template>
