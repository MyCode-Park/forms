<template>
  <div class="container mt-5">
    <div class="row">
      <div class="offset-fluid-5">
        <div class="form-group" v-for="(email, index) in emails" :key="index">
          <input
            type="email"
            class="form-control mb-3"
            v-model="email.value"
            @input="validateEmail(email)"
            :placeholder="'Email ' + (index + 1)"
          />
          <button v-if="index > 0" class="btn btn-danger btn-sm mb-2" @click="removeEmail(index)">
            Delete
          </button>
        </div>
        <div class="row justify-content-around">
          <button class="col-5 btn btn-success btn-sm mb-2" @click="addEmail">Add More</button>
          <button class="col-5 btn btn-primary btn-sm mb-2" @click="submitForm" :disabled="!isFormValid">
            Submit
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.bundle.min'
export default {
  data() {
    return {
      emails: [{ value: '' }]
    }
  },
  computed: {
    isFormValid() {
      return this.emails.every((email) => email.valid) || this.emails.length === 0
    }
  },
  methods: {
    addEmail() {
      this.emails.push({ value: '' })
    },
    removeEmail(index) {
      this.emails.splice(index, 1)
    },
    validateEmail(email) {
      email.valid = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email.value)
    },
    submitForm() {
      if (this.isFormValid) {
        const validEmails = this.emails.filter((email) => email.valid).map((email) => email.value)
        console.log('Valid Emails:', validEmails)
      }
    }
  }
}
</script>

<style scoped>
body {
  background-color: white;
}
</style>
