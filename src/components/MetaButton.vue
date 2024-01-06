<script setup>
// this takes drehimself's example with EditButton component - and adds the necessary funcitonality..
const showit = (msgg) => {
  console.log(msgg); //todo: remove this after debugging
  alert(msgg);
}

const props = defineProps({
  displaydata: String,
  metadata: String,
});
</script>

<template>
  <span :title="`${metadata}`" 
  class="text-indigo-600 hover:text-indigo-500" 
  v-on:click=showit(metadata);
  >
  {{ displaydata }}&nbsp;&#9432;
  </span>
</template>
