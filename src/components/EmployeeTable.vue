<template>
  <div class="employee-table">
    <h2>EmployeeTable</h2>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.id">
          <td v-if="editing === employee.id">
            <input type="text" v-model="employee.name" />
          </td>
          <td v-else>{{employee.name}}</td>

          <td v-if="editing === employee.id">
            <input type="text" v-model="employee.email" />
          </td>
          <td v-else>{{employee.email}}</td>

          <td v-if="editing === employee.id">
            <button @click="editEmployee(employee)">Save</button>
            <button @click="cancelEdit(employee)">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(employee)">Edit</button>
            <button @click="$emit('delete:employee', employee.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "employee-table",
  props: {
    employees: Array,
  },
  data() {
    return {
      editing: null,
      cachedEmployee: null,
    };
  },
  methods: {
    editMode: function (employee) {
      //   console.log(id);
      this.editing = employee.id;
      this.cachedEmployee = Object.assign({}, employee);
      console.log(this.cachedEmployee);
    },
    editEmployee: function (employee) {
      this.$emit("edit:employee", employee);
      this.editing = null;
    },
    cancelEdit: function (employee) {
      console.log(employee);
      Object.assign(employee, this.cachedEmployee);
      this.editing = null;
    },
  },
};
</script>

<style lang='scss' scoped>
button {
  margin-right: 2rem;
}
</style>
