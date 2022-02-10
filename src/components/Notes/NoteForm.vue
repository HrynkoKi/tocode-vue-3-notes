<template>
  <p class="message-error" v-if="messageError">{{ messageError }}</p>

  <form class="note-form" @submit.prevent>
    <textarea v-model.trim="value" placeholder="" required />
    <button @click="onSubmit" type="submit" class="btn btnPrimary">
      Add new note
    </button>
  </form>
</template>

<script>
export default {
  name: '',
  emits: ['onSubmit'],
  data() {
    return {
      value: '',
      messageError: ''
    };
  },
  methods: {
    onSubmit() {
      const value = this.value;
      const id = Math.random();

      const validationResult = this.validateField(value, value.length);

      if (validationResult) return;

      this.$emit('onSubmit', { id, value });

      this.clearFields();
    },
    clearFields() {
      this.value = '';
      this.messageError = '';
    },
    validateField(string, length) {
      if (!string) {
        this.messageError = 'The field is required!';

        return true;
      } else if (length >= 14) {
        this.messageError = 'Too long string!';

        return true;
      }

      return false;
    }
  }
};
</script>

<style lang="scss">
.note-form {
  display: flex;
  flex-direction: column;

  margin-bottom: 40px;
}

.message-error {
  text-align: center;
  color: #ff0000;
  font-size: 28px;
  font-weight: 700;
  margin-bottom: 20px;
}
</style>
