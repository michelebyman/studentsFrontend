<template>
  <div id="student-form">
    <form @submit.prevent="handleSubmit">
      <label>Student name</label>
      <input
        v-model="newStudent.student.name"
        type="text"
        ref="first"
        :class="{ 'has-error': submitting && invalidName }"
        @focus="clearStatus"
        @keypress="clearStatus"
      >

      <label>Student Email</label>
      <input
        v-model="newStudent.student.email"
        type="text"
        :class="{ 'has-error': submitting && invalidEmail }"
        @focus="clearStatus"
      >

      <label>Student Street</label>
      <input 
          v-model="newStudent.student.address.street " 
          type="text"
          :class="{ 'has-error': submitting && invalidStreet }"
          @focus="clearStatus"
          >

      <label>Student Zip Code</label>
      <input 
          v-model="newStudent.student.address.city" 
          type="text"
          :class="{ 'has-error': submitting && invalidCity }"
          @focus="clearStatus"
          >

      <label>Student City</label>
      <input 
          v-model="newStudent.student.address.zipCode" 
          type="text"
          :class="{ 'has-error': submitting && invalidZipCode }"
          @focus="clearStatus"
          >

      <p v-if="error && submitting" class="error-message">❗Please fill out all required fields</p>
      <p v-if="success" class="success-message">✅  Student successfully added</p>

      <button>Add Student</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "student-form",
  data() {
    return {
      submitting: false,
      error: false,
      success: false,

      //Wrap object to post in new object otherwise error
      newStudent: {
        student: {
          address: {
            street: "",
            zipCode: "",
            city: ""
          },
          email: "",
          name: ""
        }
      }
    };
  },
  methods: {
    handleSubmit() {
      this.submitting = true;
      this.clearStatus()
      if (
        this.invalidName ||
        this.invalidEmail ||
        this.invalidStreet ||
        this.invalidZipCode ||
        this.invalidCity
      ) {
        this.error = true;
        return;
      }

      this.$emit("add:student", this.newStudent);
      this.$refs.first.focus()

      this.newStudent = {
        student: {
          name: "",
          email: "",
          address: {
            street: "",
            zipCode: "",
            city: ""
          }
        }
      };

      
      this.error = false;
      this.success = true;
      this.submitting = false;
    },
    clearStatus() {
      this.success = false;
      this.error = false;
 
    }
  },
  computed: {
    invalidName() {
      return this.newStudent.student.name === "";
    },

    invalidEmail() {
      return this.newStudent.student.email === "";
    },

    invalidStreet() {
      return this.newStudent.student.address.street === "";
    },

    invalidZipCode() {
      return this.newStudent.student.address.zipCode === "";
    },

    invalidCity() {
      return this.newStudent.student.address.city === "";
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
button:focus {
  background: #009435;
  border: 1px solid #009435;
  outline: none;
}
</style>