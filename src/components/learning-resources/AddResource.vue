<template>
<base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
  <template #default>
    <p>At least one input field is invalid</p>
    <p>Please fill in all fields</p>
  </template>
  <template #actions>
    <base-button @click="confirmError">Ok</base-button>
  </template>
</base-dialog>
  <base-card>
    <form @submit.prevent="addNewResource">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="enteredTitle"/>
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" name="description" rows="3" ref="enteredDescription"></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="enteredLink"/>
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
import BaseDialog from '../UI/BaseDialog.vue';
export default {
  components: { BaseDialog, BaseButton },
  inject: ['addAResource'],
  data() {
    return {
      inputIsInvalid: false
    };
  },
  methods: {
    addNewResource(){
      const titleInput = this.$refs.enteredTitle.value;
      const descInput = this.$refs.enteredDescription.value;
      const linkInput = this.$refs.enteredLink.value;

      if (titleInput.trim() === '' || descInput.trim() === '' || linkInput.trim() === '') {
        this.inputIsInvalid = true;
        return;
      }
      this.addAResource(titleInput, descInput, linkInput);
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
  }
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
