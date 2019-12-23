<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <p v-if="employees.length < 1">There are no Employess on the list</p>
        <table class="table" v-else>
          <thead class="thead-dark">
            <tr>
              <th scope="col">Name</th>
              <th scope="col">Email</th>
              <th scope="col">Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="employee in employees" :key="employee.id">
              <th scope="row" v-if="editing === employee.id">
                <input type="text" class="form-control" v-model="employee.name" />
              </th>
              <th scope="row" v-else>{{ employee.name }}</th>
              <td v-if="editing === employee.id">
                <input type="text" class="form-control" v-model="employee.email" />
              </td>
              <td v-else>{{ employee.email }}</td>
              <td v-if="editing === employee.id">
                <button class="btn btn-dark mx-1" @click="editEmployee(employee)">Save</button>
                <button class="btn btn-dark" @click="editing = null">Cancel</button>
              </td>
              <td v-else>
                <button class="btn btn-dark mx-1" @click="editMode(employee.id)">Edit</button>
                <button class="btn btn-dark" @click="$emit('delete:employee', employee.id)">Delete</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "employee-table",
  data() {
    return {
      editing: null
    };
  },
  props: {
    employees: Array
  },
  methods: {
    editMode(id) {
      this.editing = id;
    },
    editEmployee(employee) {
      if (employee.name === "" || employee.email === "")
        return this.$emit("edit:employee", employee);
    }
  }
};
</script>

<style scoped></style>
