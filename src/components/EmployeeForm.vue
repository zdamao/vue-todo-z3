<template>
  <div class="employee-form">
    <h2>EmployeeForm</h2>
    <form @submit.prevent="handleSubmit">
      <label for="name">Name</label>
      <input type="text" id="name" />
      <label for="email">Email</label>
      <input type="text" id="email" />
      <button>Submit</button>
    </form>
  </div>
</template>


<script>
export default {
  name: "employee-form",
  methods: {
    handleSubmit: function () {
      console.log("handlesubmit");
    },
  },
};
</script>

<style lang='scss' scoped>
form {
  text-align: left;
}
</style>
