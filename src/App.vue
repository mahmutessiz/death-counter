<script setup lang="ts">
import { ref } from "vue";
const count = ref(0);
</script>

<template>
  <div style="
     display: flex;
     flex-direction: row;
     flex-wrap: nowrap;
     justify-content: center;
     align-items: center;
     background-color: black;">

    <button
     style="
     color: aliceblue;
     background-color: black;
     font-size: 72px;
     font-weight: 900;
     border: 0;
     cursor: zoom-in;
     width: 100%;
     "
     @click="count++">{{ count }}</button>
     <div style="font-size: 48px; font-weight: 900;
     cursor: zoom-out;" @click="count--">☠️</div>
  </div>
</template>