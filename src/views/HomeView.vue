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
  <div class="container">
    <div class="row justify-content-center" style="height: 200px">
      <div
        class="col-3 h-100 d-flex align-items-center"
        v-for="item in items"
        :key="item.id"
      >
        <div
          class="d-flex justify-content-start align-items-end pic_dt2 shadow"
          :style="
            'background-image:url(https://api.opendota.com' + item.img + ')'
          "
        >
          <div
            class="row justify-content-center align-items-center w-100"
            style="
              margin-left: 0;
              background: rgb(0, 0, 0);
              background: linear-gradient(
                0deg,
                rgba(0, 0, 0, 1) 15%,
                rgba(0, 212, 255, 0) 100%
              );
            "
          >
            <div
              class="d-flex justify-content-start ms-2 mb-1 align-items-center"
              style="color: white; font: 400"
            >
              <div v-if="item.primary_attr == 'str'">
                <img
                  src="https://cdn.cloudflare.steamstatic.com/apps/dota2/images/dota_react/icons/hero_strength.png"
                  alt="str"
                />
              </div>
              <div v-if="item.primary_attr == 'agi'">
                <img
                  src="https://cdn.cloudflare.steamstatic.com/apps/dota2/images/dota_react/icons/hero_agility.png"
                  alt="agi"
                />
              </div>
              <div v-if="item.primary_attr == 'int'">
                <img
                  src="https://cdn.cloudflare.steamstatic.com/apps/dota2/images/dota_react/icons/hero_intelligence.png"
                  alt="int"
                />
              </div>
              <div class="ms-2" style="font-size: 20px">
                {{ item.localized_name }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.pic_dt2 {
  position: absolute;
  height: 150px;
  width: 260px;
  background-size: 260px 150px;
  transition: all 0.4s;
  -moz-transition: all 0.4s;
  -webkit-transition: all 0.4s;
  -o-transition: all 0.4s;
  background-repeat: no-repeat;
  z-index: 0;
}
.pic_dt2:hover {
  position: absolute;
  height: 170px;
  width: 290px;
  background-size: 290px 170px;
  transition: all 0.4s;
  -moz-transition: all 0.4s;
  -webkit-transition: all 0.4s;
  -o-transition: all 0.4s;
  background-repeat: no-repeat;
  z-index: 1;
  margin-left: -15px;
}
</style>
