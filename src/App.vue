<template>
  <button @click="mypopup">Open Popup...</button>
  <!-- embed  type="text/plain" src="./assets/text.txt" /      geht nicht -->
  <p>Filter val in App.vue: {{ myFilVal }}</p>
  <Table
    :myfields="myfields"
    :studentData="studentDatax"
    :myFilter="myFilVal"
  ></Table>

  <div ref="myModal" class="modal">
    <div class="modal-content">
      <span class="close" @click="mypopup">&times;</span>
      <p>Enter number to filter age for</p>
      <myInput @setfilterto="setfilter" />
    </div>
  </div>
</template>

<script>
import Table from "./components/table.vue";
import myInput from "./components/input.vue";

export default {
  name: "App",
  components: {
    Table,
    myInput,
  },
  methods: {
    setfilter(fil_) {
      console.log("filterxxx" + fil_);
      this.myFilVal = Number(fil_);
    },
    mypopup() {
      //this.$refs.myModal.style="display:block";
      if (this.$refs.myModal.style.display === "block")
        this.$refs.myModal.style = "display:none";
      else this.$refs.myModal.style = "display:block";
      //console.log(this.$refs.myModal.style);
    },
  },

  data() {
    return {
      myFilVal: "23",
      //  isSorted: 0...not sorted, 1...ASC, -1...DESC
      // sortBy: 0...number, 1...text
      myfields: [
        { label: "ID", isSorted: 0, sortBy: 0 },
        { label: "Name", isSorted: 0, sortBy: 1 },
        { label: "Course", isSorted: 0, sortBy: 1 },
        { label: "Gender", isSorted: 0, sortBy: 1 },
        { label: "Age", isSorted: 0, sortBy: 0 },
      ],

      studentDatax: [
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
      ],
    };
  },
};
</script>

<style>
.modal {
  display: none; /* Hidden by default */
  //display: block; /* shown by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 100px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0, 0, 0); /* Fallback color */
  background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
}

/* Modal Content */
.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
  box-shadow: 0px 0px 10px 10px cyan;
}

/* The Close Button */
.close {
  color: #aaaaaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}
</style>