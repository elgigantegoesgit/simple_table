<template>
  <table>
    <thead>
      <tr>
        <!-- loop through each value of the fields to get the table header -->
        <th v-for="field in fields" :key="field" @click="sortTable(field)">
          {{ field }}
          <i v-if="sortDesc">▼</i>
          <i v-else>▲</i>
        </th>
      </tr>
    </thead>

    <tbody>
      <!-- Loop through the list get the each student data -->
      <tr v-for="item in studentData" :key="item">
        <td v-for="field in fields" :key="field">{{ item[field] }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "TableComponent",
  props: {
    studentData: {
      type: Array,
    },
    fields: {
      type: Array,
    },
  },
  data() {
    return {
      sortDesc: true,
    };
  },
  methods: {
    sortTable(field) {
      this.sortDesc = !this.sortDesc;
      console.log("sort " + this.sortDesc + " by " + field);
    },
  },
};
</script>

<style scoped>
table,
th,
td {
  border: solid 2px;
  border-color: rgb(13, 124, 109);
  border-collapse: collapse;
}
tr:nth-child(even) {
  background-color: #cff1f7;
}
th {
  background-color: #bce9f1;
}
</style>