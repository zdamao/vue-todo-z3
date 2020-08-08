<template>
  <div class="employee-form">
    <h2>EmployeeForm</h2>
    <form @submit.prevent="handleSubmit">
      <label for="name">Name</label>
      <input
        type="text"
        id="name"
        v-model="employee.name"
        @focus="clearStatus"
        @keyup="clearStatus"
        ref="first"
        v-bind:class="{'has-error': isValidName && submitting}"
      />
      <label for="email">Email</label>
      <input
        type="text"
        id="email"
        v-model="employee.email"
        @focus="clearStatus"
        v-bind:class="{'has-error': isValidEmail && submitting}"
      />
      <p v-if="error">error</p>
      <p v-if="success">success</p>
      <button>Submit</button>
    </form>
  </div>
</template>


<script>
export default {
  name: "employee-form",
  data() {
    return {
      submitting: false,
      error: false,
      success: false,
      employee: {
        name: "",
        email: "",
      },
    };
  },
  computed: {
    isValidName: function () {
      return this.employee.name === "";
    },
    isValidEmail: function () {
      return this.employee.email === "";
    },
  },
  methods: {
    handleSubmit: function () {
      this.submitting = true;
      this.clearStatus();
      if (this.isValidName || this.isValidEmail) {
        this.error = true;
        return;
      }
      this.$emit("add:employee", this.employee);
      this.employee = {
        name: "",
        email: "",
      };
      this.error = false;
      this.$refs.first.focus();
      this.success = true;
      this.submitting = false;
    },
    clearStatus: function () {
      this.error = false;
      this.success = false;
    },
  },
};
</script>

<style lang='scss' scoped>
form {
  text-align: left;
}
</style>
