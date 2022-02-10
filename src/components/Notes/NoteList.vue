<template>
  <ul class="note-list">
    <li class="note-item" v-for="(note, index) in notes" :key="note.id">
      <div class="note-header">
        <p
          class="note-header__value"
          @input="editNote($event, index)"
          :contenteditable="edit"
        >
          {{ note.value }}
        </p>
        <span @click="remove(note.id)" class="note-header__close">
          &times;
        </span>
      </div>
      <!-- <p class="note-footer"></p> -->
    </li>
  </ul>
</template>

<script>
export default {
  name: 'NoteList',
  data() {
    return {
      edit: true
    };
  },
  props: {
    notes: {
      type: Array,
      required: true
    }
  },
  methods: {
    remove(id) {
      this.$emit('remove', id);
    },
    editNote(event, index) {
      let note = this.notes[index];
      note.value = event.target.textContent;

      this.$emit('editNote', { note, index });
    }
  }
};
</script>

<style lang="scss">
.notes-list {
  padding: 40px 0;
}
.note-item {
  width: 100%;
  padding: 18px 20px;
  margin-bottom: 20px;
  border-radius: 14px;
  background-color: #ffffff;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.02);
  &:hover {
    box-shadow: 0 30px 30px rgba(0, 0, 0, 0.04);
    transform: translate(0, -6px);
    transition-delay: 0s !important;
  }
}
.note-header {
  display: flex;
  align-items: center;

  &__value {
    margin-right: auto;
  }

  &__close {
    display: block;
    font-size: 28px;
    cursor: pointer;
    padding: 5px 10px;
  }
}
.note-footer {
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: start;
}
</style>
