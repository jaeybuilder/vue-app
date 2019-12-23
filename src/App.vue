<template>
  <div id="app">
    <img class="d-block mx-auto" alt="Vue logo" src="./assets/logo.png" />
    <div class="small-container">
      <h1 class="text-center">Employees App</h1>
      <employee-form @add:employee="addEmployee" />
      <employee-table
        v-bind:employees="employees"
        @delete:employee="deleteEmployee"
        @edit:employee="editEmployee"
      />
    </div>
  </div>
</template>

<script>
import EmployeeTable from "./components/EmployeeTable.vue";
import EmployeeForm from "./components/EmployeeForm.vue";

export default {
  name: "app",
  components: {
    EmployeeTable,
    EmployeeForm
  },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: "Jairo",
          email: "jairomgr@gmail.com"
        },
        {
          id: 2,
          name: "Maria",
          email: "maripau86@gmail.com"
        }
      ]
    };
  },
  methods: {
    addEmployee(employee) {
      const lastId =
        this.employees.length > 0
          ? this.employees[this.employees.length - 1].id
          : 0;

      const id = lastId + 1;
      const newEmployee = { ...employee, id };

      this.employees = [...this.employees, newEmployee];
    },
    deleteEmployee(id) {
      this.employees = this.employees.filter(ele => {
        return ele.id !== id;
      });
    },
    editEmployee(employee) {
      this.employees = this.employees.map(ele => {
        ele.id === employee.id ? employee : ele;
      });
    }
  }
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
