<template>
  <div id="app">
    <app-header></app-header>
    <div id="appContainer">
      <speech />
      <note-item></note-item>
    </div>
  </div>
</template>
<script>
import appHeader from "@/components/appHeader";
import noteItem from "@/components/noteItem";
import speech from "@/components/speech";
export default {
  components: {
    appHeader,
    noteItem,
    speech,
  },
};
</script>