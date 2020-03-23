<template>
  <div id="farm-form">
    <form @submit.prevent="handleSubmit">
      <label>Farm name</label>
      <input
        ref="first"
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        v-model="farm.name"
        @focus="clearStatus"
        @keypress="clearStatus"
      />
      <label>Farm Email</label>
      <input
        type="text"
        :class="{ 'has-error': submitting && invalidEmail }"
        v-model="farm.email"
        @focus="clearStatus"
      />
      <p v-if="error && submitting" class="error-message">❗Please fill out all required fields</p>
      <p v-if="success" class="success-message">✅ Farm successfully added</p>
      <button>Add Farm</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "farm-form",
  data() {
    return {
      submitting: false,
      error: false,
      success: false,
      farm: {
        name: "",
        email: ""
      }
    };
  },
  computed: {
    invalidName() {
      return this.farm.name === "";
    },

    invalidEmail() {
      return this.farm.email === "";
    }
  },
  methods: {
    handleSubmit() {
      this.submitting = true;
      this.clearStatus();

      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }

      this.$emit("add:farm", this.farm);
      this.$refs.first.focus()

      this.farm = {
        name: "",
        email: ""
      };

      this.error = false;
      this.success = true;
      this.submitting = false;
    },

    clearStatus() {
      this.success = false;
      this.error = false;
    }
  }
};
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}

[class*="-message"] {
  font-weight: 500;
}

.error-message {
  color: #d33c40;
}

.success-message {
  color: #32a95d;
}
</style>