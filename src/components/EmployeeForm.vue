<template>
  <div id="employee-form" class="container">
    <div class="row">
      <div class="col-lg">
        <div class="form-group">
          <label for>Employee Name</label>
          <input class="form-control" ref="first" v-model="employee.name" type="text" />
        </div>
        <div class="form-group">
          <label for>Employee email</label>
          <input class="form-control" v-model="employee.email" type="text" />
        </div>
        <div class="form-group">
          <button class="btn btn-success" @click="handleSubmit">Add Employee</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "employee-form",
  data() {
    return {
      employee: {
        name: "",
        email: ""
      }
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("add:employee", this.employee);
      this.$refs.first.focus();
    }
  }
};
</script>

<style scoped>
label {
  text-align: left !important;
}

[class*="-message"] {
  font-weight: 500;
}

.error-msg {
  color: #d33c40;
}

.succes-msg {
  color: #32a95d;
}
</style>
