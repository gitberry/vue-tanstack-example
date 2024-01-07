<script setup>
// this takes drehimself's example with EditButton component - and adds the necessary funcitonality..
const showit = (msgg) => {
  console.log(msgg); //todo: remove this after debugging
  alert(msgg);
};
const truncit = (msgg,msggmax) => {
  if (msgg.length > msggmax ) msgg = msgg.substring(0,msggmax) + ' ...';
  return msgg;
}

const props = defineProps({
  displaydata: String,
  metadata: String, 
  dispmax: Number, 
});
</script>

<template>
  <span :title="`${metadata}`" 
  class="text-indigo-600 hover:text-indigo-500" 
  v-on:click=showit(metadata);
  >
  {{ truncit(displaydata,dispmax) }}
  </span>
</template>
