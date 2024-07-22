<script setup lang="ts">
import { ref, onMounted } from "vue";
import { appWindow } from "@tauri-apps/api/window";

const count = ref(0);

onMounted(async() => {
  await appWindow.setAlwaysOnTop(true);
});
</script>

<template>
  <div data-tauri-drag-region
   style="
        display: flex;
        justify-content: end;
        width: 100%;
        height: 25px;
        padding: 0;
        background-color: rgba(0, 0, 0, 0.7);
        border-radius: 10px 10px 0 0;
        z-index: 1;
          ">
    <button @click="appWindow.close()"
     style="
        width: 50px;
        padding: 0; 
        font-size: small;
        color: aliceblue;
        background-color: transparent;
        border: 0;
        cursor: pointer;
        ">
        x
      </button>
  </div>
  <div style="
     display: flex;
     flex-direction: row;
     flex-wrap: nowrap;
     justify-content: center;
     align-items: center;
     background-color: rgba(0, 0, 0, 0.7);
     border-radius: 0 0 10px 10px;
     overflow: hidden;
     padding: 10px;
     z-index: 0;
     margin-top: -10px;
     ">

    <button
     style="
     color: aliceblue;
     background-color: transparent;
     font-size: 72px;
     font-weight: 900;
     border: 0;
     cursor: zoom-in;
     width: 100%;
     "
     @click="count++">{{ count }}&nbsp;</button>
     <button style="font-size: 48px; background-color: transparent; border: 0; font-weight: 900;
     cursor: zoom-out;" @click="count--">☠️</button>
  </div>
</template>