<template>
  <div class="new-note">
    <label for="title">Title</label>
    <input name="title" v-model="note.title" type="text" />
    <label for="descr">Description</label>
    <textarea name="descr" v-model="note.descr"></textarea>
    <button class="btn btnPrimary" @click="addNote">New note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true
    }
  },
  methods: {
    addNote() {
      this.$emit('addNote', this.note)
    }
  }
}
</script>

<style lang="scss">
.new-note {
  text-align: center;
}
.btn {
  margin-top: 25px;
}
</style>
