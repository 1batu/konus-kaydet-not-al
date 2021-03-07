<template>
  <div class="speech_container">
    <i
      class="fa fa-microphone fa-3x"
      :class="{ isListening }"
      @click="listen"
    ></i>
    <p v-if="speechToText !== null" class="speechToText">
      {{ speechToText }}
    </p>
  </div>
</template>
<script>
export default {
  props: {
    addNote: {
      type: Function,
      required: true,
    },
    deleteNote: {
      type: Function,
      required: true,
    },
    removeAllNotes: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      speechToText: null,
      isListening: false,
      recognition: null,
    };
  },
  mounted() {
    this.recognition = new webkitSpeechRecognition();
    this.recognition.lang = "tr";
    this.recognition.onresult = this.record;
  },
  methods: {
    listen() {
      this.isListening = true;
      this.recognition.start();
    },
    record(event) {
      this.isListening = false;
      this.speechToText = event.results[0][0].transcript;

      const parseRegex = /(?<id>(\d*))\s(?=nolu).*(?<command>(sil))$/giu;
      const voiceMatch = parseRegex.exec(this.speechToText);

      const allNoteRemoveRegex = /tüm notları sil/giu;
      const allNoteRemoveMatch = allNoteRemoveRegex.test(this.speechToText);

      setTimeout(() => {
        //voiceMatch && voiceMatch.groups.id && voiceMatch.groups.groups
        if (voiceMatch) {
          this.deleteNote(voiceMatch.groups.id);
        } else if (allNoteRemoveMatch) {
          this.removeAllNotes();
        } else {
          this.addNote(event.results[0][0].transcript);
        }
        this.speechToText = null;
      }, 1000);
    },
  },
};
</script>
<style scoped>
i {
  cursor: pointer;
}
.speechToText {
  margin-top: 10px;
}
.isListening {
  color: #c00201;
  transition: all 0.5s;
}
</style>