<template>
  <div id="app">
    <employee-form @add:employee="addEmployee" />
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
      employees: [],
    };
  },
  methods: {
    //get
    getEmployees: async function() {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );
        const data = await response.json();
        this.employees = data;
      } catch (error) {
        console.log(error);
      }
    },
    //post
    addEmployee: async function(employee) {
      // console.log(employee);
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users",
          {
            method: "POST",
            body: JSON.stringify(employee),
            headers: { "Content-Type": "application/json; charset=UTF-8" },
          }
        );
        const data = await response.json();
        this.employees = [...this.employees, data];
      } catch (error) {
        console.log(error);
      }
    },
    // addEmployee: function(employee) {
    //   // console.log(employee);
    //   const lastId = this.employees[this.employees.length - 1].id;
    //   const id = lastId + 1;
    //   const newEmployee = { ...employee, id };
    //   this.employees = [...this.employees, newEmployee];
    // },

    // put -> but has 500 error, even cp, i dont konw why
    editEmployee: async function(id, updatedEmployee) {
      try {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/users/${id}`,
          {
            method: "PUT",
            body: JSON.stringify(updatedEmployee),
            headers: { "Content-Type": "application/json charset=UTF-8" },
          }
        );
        const data = await response.json();
        this.employees = this.employees.map((employee) => {
          return employee.id === id ? data : employee;
        });
      } catch (error) {
        console.log(error);
      }
    },
    // editEmployee: function(id, updatedEmployee) {
    //   console.log(id, updatedEmployee);
    //   this.employees = this.employees.map((employee) => {
    //     return employee.id === id ? updatedEmployee : employee;
    //   });
    // },

    //delete
    deleteEmployee: async function(id) {
      try {
        await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
          method: "DELETE",
        });
        this.employees = this.employees.filter((employee) => {
          return employee.id !== id;
        });
      } catch (error) {
        console.log(error);
      }
    },
    // deleteEmployee: function(id) {
    //   this.employees = this.employees.filter((employee) => {
    //     return employee.id !== id;
    //   });
    // },
  },
  mounted() {
    this.getEmployees();
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
