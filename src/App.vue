<template>
  <div id="app">
    <app-header></app-header>
    <div id="appContainer">
      <speech
        :addNote="addNote"
        :deleteNote="deleteNote"
        :removeAllNotes="removeAllNotes"
      />
      <note-item v-for="not in notes" :key="not.id" :noteItem="not"></note-item>
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
  data() {
    return {
      nnotes: [
        { id: 1, note: "Burası not alanı 1" },
        { id: 2, note: "Burası not alanı 2" },
        { id: 3, note: "Burası not alanı 3" },
        { id: 4, note: "Burası not alanı 4" },
        { id: 5, note: "Burası not alanı 5" },
      ],
      notes: [],
    };
  },
  methods: {
    addNote(note) {
      this.notes.push({
        id: this.notes.length + 1,
        note: note,
      });
    },
    deleteNote(id) {
      this.notes.splice(
        this.notes.findIndex((n) => n.id == id),
        1
      );
    },
    removeAllNotes() {
      this.notes = [];
    },
  },
};
</script>