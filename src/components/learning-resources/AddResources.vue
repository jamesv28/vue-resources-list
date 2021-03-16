<template>
  <base-dialog v-if="inputisInvalid" title="input is invalid" @close="removeDialog">
    <template #default>
      <p>Unfortunately, at least one input is invalid</p>
      <p>Please make sure all fields have been entered</p>
    </template>
    <template #actions>
      <base-button @click="removeDialog">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title: </label>
        <input id="title" type="text" name="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description: </label>
        <textarea
          id="description"
          type="text"
          name="description"
          rows="3"
          ref="descInput"
        />
      </div>
      <div class="form-control">
        <label for="link">Link: </label>
        <input
          id="link"
          type="url"
          name="link"
          ref="linkInput"
          placeholder="https://example.com"
          pattern="https://.*"
        />
      </div>
      <div>
        <base-button type="submit">Add resource</base-button>
      </div>
    </form>
  </base-card>
</template>
<script>
export default {
  inject: ['addResources'],
  data() {
    return {
      inputisInvalid: false
    };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDesc = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (enteredTitle === '' || enteredDesc === '' || enteredUrl === '') {
        this.inputisInvalid = true;
        return;
      }
      this.addResources(enteredTitle, enteredDesc, enteredUrl);
    },
    removeDialog() {
      this.inputisInvalid = false;
    }
  }
};
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
