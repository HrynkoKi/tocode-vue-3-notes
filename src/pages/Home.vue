<template v-slot:header>
  <div class="home">
    <div class="note-wrapper">
      <note-form @onSubmit="handleSubmit" />

      <note-list
        @remove="handleRemove"
        @editNote="handleEditNote"
        :notes="notes"
      />
    </div>
  </div>
</template>

<script>
import NoteForm from '@/components/Notes/NoteForm.vue';
import NoteList from '@/components/Notes/NoteList.vue';

export default {
  name: 'Home',
  components: { NoteForm, NoteList },
  data() {
    return {
      notes: []
    };
  },
  watch: {
    notes: {
      handler(updatedList) {
        localStorage.setItem('notes', JSON.stringify(updatedList));
      },
      deep: true
    }
  },
  methods: {
    handleSubmit(newNote) {
      this.notes.push(newNote);
    },
    handleRemove(id) {
      this.notes = this.notes.filter(note => note.id !== id);
    },
    handleEditNote(editedNote) {
      const { note, index } = editedNote;

      this.notes[index] = note;
    },
    getNotes() {
      const localList = JSON.parse(localStorage.getItem('notes'));

      if (localList) {
        this.notes = localList;

        return;
      }

      return [];
    }
  },
  mounted() {
    this.getNotes();
  }
};
</script>

<style lang="scss">
.note-wrapper {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
}
</style>
