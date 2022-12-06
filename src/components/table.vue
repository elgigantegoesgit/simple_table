<template>
  <!-- ul>
    <li v-for="item in myfields">{{ item.label }}</li>
  </ul>
  <ul>
    <li v-for="(obj, idx) in myfields">{{ idx }} : {{ obj }}</li>
  </ul -->
  <p>
    <button @click="myFilterMeth()">Filter me!</button>
    for what contains: {{ myFilter }}
  </p>
  <table>
    <thead>
      <tr>
        <!-- loop through each value of the fields to get the table header -->
        <th
          v-for="(field, idx) in myfieldslcl"
          :key="field"
          @click="sortTable(idx)"
        >
          {{ field.label }}
          <!-- i> xx {{ field.isSorted }}</i         ohter arrows: ▲▼↑↓↕ -->
          <strong v-if="field.isSorted === 0" :style="{ color: 'gray' }"
            >⬆</strong
          >
          <strong v-if="field.isSorted === 1">⬇</strong>
          <strong v-if="field.isSorted === -1">⬍</strong>
        </th>
      </tr>
    </thead>

    <tbody>
      <!-- Loop through the list get the each student data -->
      <tr v-for="item in studentDatalcl" :key="item">
        <td v-for="field in myfields" :key="field">{{ item[field.label] }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "TableComponent",
  props: {
    myFilter: String,
    myfields: {
      type: Array,
    },
    studentData: {
      type: Array,
    },
  },
  data() {
    return {
      myfieldslcl: [], // local copy of passed prop 'myfields' in order to mutate 'isSorted'
      studentDatalcl: [],
      studentDatalcl_cpy: [],
    };
  },
  methods: {
    myFilterMeth() {
      console.log("filter by" + this.myFilter);
      var fil_ = this.myFilter;
      this.studentDatalcl = [
        ...this.studentDatalcl_cpy.filter(function (el) {
          return el.Age === fil_;
        }),
      ];
    },
    sortTable(idx_) {
      this.myfieldslcl.forEach(function (myfield_, idx_loop) {
        if (idx_loop !== idx_) myfield_.isSorted = 0;
      });

      if (this.myfieldslcl[idx_].isSorted < 1)
        this.myfieldslcl[idx_].isSorted++;
      else this.myfieldslcl[idx_].isSorted = -1;

      if (this.myfieldslcl[idx_].isSorted === 0) {
        // restore original order
        this.studentDatalcl = this.studentDatalcl_cpy;
        return; // no sorting, change nothing
      }

      // console.log("sort " + this.myfieldslcl[idx_].isSorted + " by " + this.myfieldslcl[idx_].label );
      //isSorted: 0...not sorted, 1...ASC, -1...DESC
      const sort_ = this.myfieldslcl[idx_].isSorted;
      const sortFieldLabel_ = this.myfieldslcl[idx_].label;

      // sort by number
      if (this.myfieldslcl[idx_].sortBy === 0) {
        console.log("sort by " + sortFieldLabel_ + " with method nr");
        this.studentDatalcl.sort(function (a, b) {
          let x = Number(a[sortFieldLabel_]);
          let y = Number(b[sortFieldLabel_]);
          if (x < y) return -1 * sort_;
          if (x > y) return 1 * sort_;
          return 0;
        });
      }
      // sort by text/string
      else {
        console.log("sort by " + sortFieldLabel_ + " with method txt");
        this.studentDatalcl.sort(function (a, b) {
          let x = a[sortFieldLabel_].toLowerCase();
          let y = b[sortFieldLabel_].toLowerCase();
          if (x < y) return -1 * sort_;
          if (x > y) return 1 * sort_;
          return 0;
        });
      }
    },
  },
  mounted() {
    console.log("process.env.NODE_ENV set to: '" + process.env.NODE_ENV + "'");
    this.studentDatalcl = [...this.studentData];
    for (var i = 6; i < 1000; i++) {
      // ab 15000 wirds zach (>1 sec)
      this.studentDatalcl.push({
        ID: i,
        Name: "wurst",
        Course: "sudln",
        Gender: i % 2 === 0 ? "male" : "female",
        Age: 99 - i,
      });
    }
    this.studentDatalcl_cpy = this.studentDatalcl; // only copys reference(memAdress) of array, not the values - but it works?
    this.myfieldslcl = [...this.myfields];
    console.table(this.myfieldslcl[2].isSorted);
  },
};
</script>

<style scoped>
table {
  margin-left: auto;
  margin-right: auto;
}
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