<template>
  <div id="app">
    <employee-form />
    <employee-table
      :employees="employees"
      @delete:employee="deleteEmployee"
      @edit:employee="editEmployee"
    />
  </div>
</template>

<script>
import EmployeeForm from "@/components/EmployeeForm.vue";
import EmployeeTable from "@/components/EmployeeTable.vue";
export default {
  name: "App",
  components: {
    EmployeeForm,
    EmployeeTable,
  },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: "zdamao",
          email: "zdamao@126.com",
        },
        {
          id: 2,
          name: "adamao",
          email: "adamao@126.com",
        },
        {
          id: 3,
          name: "bdamao",
          email: "bdamao@126.com",
        },
      ],
    };
  },
  methods: {
    deleteEmployee: function (id) {
      this.employees = this.employees.filter((employee) => {
        return employee.id !== id;
      });
    },
    editEmployee: function (id, updatedEmployee) {
      console.log(id, updatedEmployee);
      this.employees = this.employees.map((employee) => {
        return employee.id === id ? updatedEmployee : employee;
      });
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 60%;
  margin: 0 auto;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
