<template>
  <div id="app">
    <h1 class="mb-4">Lista de angajati</h1>
    <h2>Adauga angajat</h2>
    <div>
      <input v-model="newEmployee.lastName" type="text" placeholder="Last name">
      <input v-model="newEmployee.firstName" type="text" placeholder="First name">
      <input v-model="newEmployee.age" type="text" placeholder="Age">
      <input v-model="newEmployee.department" type="text" placeholder="Department">
      <input v-model="newEmployee.employedSince" type="text" placeholder="Employeed since">
      <button @click="addNewEmployee" class="btn btn-primary">Add</button>
    </div>
    <h2 class="my-2">Filter</h2>
    <button @click="showFEemployees" class="btn btn-secondary">FE</button>
    <button @click="showBEemployees" class="mx-3 btn btn-secondary">BE</button>
    <div v-show="showFE">
      <div v-for="(employee, index) in fEemployees" v-bind:key="index"
           class="border border-3 border border-dark rounded-4 m-auto p-1 bg-light w-25 my-3">
        <div>
          <p @click="showIndexFEemployee = showIndexFEemployee === -1 ? index : -1">First name: {{
              employee.firstName
            }}</p>
          <div v-show="showIndexFEemployee === index">
            <p>Last name: {{ employee.lastName }}</p>
            <p>Age: {{ employee.age }}</p>
            <p>Department: {{ employee.department }}</p>
            <p>Employeed since: {{ employee.employedSince }}</p>
            <button @click="deleteProduct(index)" class="btn btn-danger">
              Delete
            </button>
          </div>
        </div>
      </div>
    </div>
    <div v-show="showBE">
      <div v-for="(employee, index) in bEemployees" v-bind:key="index"
           class="border border-3 border border-dark rounded-4 m-auto p-1 bg-light w-25 my-3">
        <div>
          <p @click="showIndexBEemployee = showIndexBEemployee === -1 ? index : -1">First name: {{
              employee.firstName
            }}</p>
          <div v-show="showIndexBEemployee === index">
            <p>Last name: {{ employee.lastName }}</p>
            <p>Age: {{ employee.age }}</p>
            <p>Department: {{ employee.department }}</p>
            <p>Employeed since: {{ employee.employedSince }}</p>
            <button @click="deleteProduct(index)" class="btn btn-danger">Delete</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      employees: [
        {
          firstName: "Adrian",
          lastName: "Popovici",
          age: 28,
          department: "FE",
          employedSince: 2018
        },
        {
          firstName: "Cristina",
          lastName: "Popa",
          age: 36,
          department: "BE",
          employedSince: 2010
        },
        {
          firstName: "Carol",
          lastName: "Man",
          age: 43,
          department: "FE",
          employedSince: 201
        },
        {
          firstName: "Elisa",
          lastName: "Ion",
          age: 25,
          department: "FE",
          employedSince: 2020,
        }
      ],
      newEmployee: '',
      bEemployees: [],
      fEemployees: [],
      showBE: false,
      showFE: false,
      showIndexEmployee: -1,
      showIndexFEemployee: -1,
      showIndexBEemployee: -1,
      showAllEmployee: false,
    }
  },
  methods: {
    addNewEmployee() {
      if (this.newEmployee.department === "BE") {
        this.bEemployees.push(this.newEmployee)
      }
      if (this.newEmployee.department === "FE") {
        this.fEemployees.push(this.newEmployee)
      }
      //this.employees.push(this.newEmployee)
    },
    showEmployee() {
      this.showAllEmployee = !this.showAllEmployee;
    },
    showBEemployees() {
      this.showBE = !this.showBE;
      this.showFE = false;
      this.bEemployees = this.employees.filter(employee => employee.department === "BE")
    },
    showFEemployees() {
      this.showFE = !this.showFE;
      this.showBE = false;
      this.fEemployees = this.employees.filter(employee => employee.department === "FE")
    },
    deleteProduct(employee, index) {
      if (employee[index] === this.bEemployees[index]) {
        this.bEemployees.splice(index, 1)
        this.showBE = false;
        this.showIndexBEemployee = this.showIndexBEemployee === -1 ? index : -1
      }
      if (employee[index] === this.fEemployees[index]) {
        this.fEemployees.splice(index, 1)
        this.showIndexFEemployee = this.showIndexFEemployee === -1 ? index : -1
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: cadetblue;
}

html {
  margin: auto;
  background: cadetblue;
}

input {
  margin: auto;
  margin-bottom: 3px;
  display: block;
}

</style>
