<template>
  <div class="note_item">
    <div class="id_content">
      <span>#{{ noteItem.id }}</span>
    </div>
    <div class="not_content">
      {{ noteItem.note }}
    </div>
  </div>
</template>
<script>
export default {
  props: {
    noteItem: {
      type: Object,
      required: true,
    },
  },
};
</script>