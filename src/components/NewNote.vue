<template>
  <div class="new-note">
    <label for="title">Title</label>
    <input
      :style="{backgroundColor: note.color}"
      id="title"
      v-model="note.title"
      type="text"
    />
    <label for="descr">Description</label>
    <textarea
      :style="{backgroundColor: note.color}"
      id="descr"
      v-model="note.descr"
    ></textarea>

    <div
      class="color-palette"
      v-for="(color, index) in colorPalette"
      :key="index"
    >
      <input
        :id="color"
        type="radio"
        :value="color"
        v-model="note.color"
        name="color"
      />
      <label
        class="color"
        :for="color"
        :style="{backgroundColor: color}"
      ></label>
    </div>

    <button class="btn btnPrimary" @click="addNote">New note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true
    },
    colorPalette: {
      type: Array,
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

<style lang="scss" scoped>
.active {
  border: 2px solid #000;
}
input[type='radio'] {
  display: none;
}
.color-palette {
  display: inline-block;
}
.color {
  border: 1px solid #555;
  width: 40px;
  height: 40px;
  margin: 20px;
}
.new-note {
  text-align: center;
}
.btn {
  display: block;
  margin: 30px auto;
}
</style>
