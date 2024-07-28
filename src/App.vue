<script setup lang="ts">
import { ref, onMounted } from "vue";
import { appWindow } from "@tauri-apps/api/window";
import { Store } from "tauri-plugin-store-api";

const store = new Store(".settings.dat");
const deaths: any = ref(0);

onMounted(async () => {
  await appWindow.setAlwaysOnTop(true);
  const deathCount = await store.get("deaths");
  if (deathCount) {
    deaths.value = deathCount;
  } else {
    deaths.value = 0;
  }
  console.log(deaths.value);
});
</script>

<template>
  <div
    style="
      background-color: rgba(0, 0, 0, 0.7);
      border-radius: 10px;
      overflow: hidden;
    "
  >
    <div
      data-tauri-drag-region
      style="
        display: flex;
        justify-content: end;
        width: 100%;
        height: 25px;
        padding: 0;
        border-radius: 10px 10px 0 0;
        z-index: 1;
      "
    >
      <button
        @click="appWindow.close()"
        style="
          width: 50px;
          padding: 0;
          font-size: small;
          color: aliceblue;
          background-color: transparent;
          border: 0;
          cursor: pointer;
        "
      >
        x
      </button>
    </div>
    <div
      style="
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        justify-content: center;
        align-items: center;
        padding: 10px;
        z-index: 0;
        margin-top: -10px;
      "
    >
      <button
        style="
          color: aliceblue;
          background-color: transparent;
          font-size: 48px;
          font-weight: 900;
          border: 0;
          cursor: pointer;
        "
        @click="
          async () => {
            await store.set('deaths', deaths - 1);
            deaths--;
            await store.save();
          }
        "
      >
        {{ deaths }}&nbsp;
      </button>
      <button
        style="
          font-size: 44px;
          background-color: transparent;
          border: 0;
          font-weight: 900;
          cursor: pointer;
        "
                @click="
          async () => {
            await store.set('deaths', deaths + 1);
            deaths++;
            await store.save();
          }
        "
      >
        ☠️
      </button>
    </div>
  </div>
</template>
