<template>
  <Table :myfields="myfields" :studentData="studentData"></Table>
</template>

<script>
import Table from "./components/table.vue";

export default {
  name: "App",
  components: {
    Table,
  },

  setup() {
    var myfields = [];
    myfields.push({ label: "ID", isSorted: 0, sortBy: 0 }); // isSorted: 0...not sorted, 1...ASC, -1...DESC
    myfields.push({ label: "Name", isSorted: 0, sortBy: 1 }); // sortBy: 0...number, 1...text
    myfields.push({ label: "Course", isSorted: 0, sortBy: 1 });
    myfields.push({ label: "Gender", isSorted: 0, sortBy: 1 });
    myfields.push({ label: "Age", isSorted: 0, sortBy: 0 });

    //An array of values for the data
    const studentData = [
      {
        ID: "01",
        Name: "Abiola Esther x",
        Course: "Computer Science",
        Gender: "Female",
        Age: "27",
      },
      {
        ID: "02",
        Name: "Robert V. Kratz",
        Course: "Philosophy",
        Gender: "Male",
        Age: "21",
      },
      {
        ID: "03",
        Name: "Kristen Anderson",
        Course: "Economics",
        Gender: "Female",
        Age: "23",
      },
      {
        ID: "04",
        Name: "Adam Simon",
        Course: "Food science",
        Gender: "Male",
        Age: "22",
      },
      {
        ID: "05",
        Name: "Daisy Katherine",
        Course: "Business studies",
        Gender: "Female",
        Age: "19",
      },
    ];

    return { studentData, myfields };
  },
};
</script>