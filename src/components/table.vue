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
      sortDescFields: new Array(this.fields.length).fill(0),
      myfields: [],
    };
  },
  methods: {
    sortTable(field) {
      this.sortDesc = !this.sortDesc;
      console.log("sort " + this.sortDesc + " by " + field);
      console.log(this.sortDescFields);
      console.log(this.myfields[2]);
    },
  },
  mounted() {
    console.log("process.env.NODE_ENV set to: '" + process.env.NODE_ENV + "'");
    console.log(this.sortDescFields);

    this.myfields.push({ label: "ID", isSorted: 0 });
    this.myfields.push({ label: "Name", isSorted: 0 });
    this.myfields.push({ label: "Course", isSorted: 0 });
    this.myfields.push({ label: "Gender", isSorted: 0 });
    this.myfields.push({ label: "Age", isSorted: 0 });
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