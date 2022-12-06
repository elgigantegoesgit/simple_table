<template>
  <p>Message is: '{{ myVal }}'</p>
  <input v-model.lazy="myVal" placeholder="edit me" />
</template>

<script>
export default {
  emits: ["setfilterto"],
  name: "InputComponent",
  props: {},
  data() {
    return {
      myVal: "",
    };
  },
  methods: {},
  watch: {
    myVal(newVal, oldVal) {
      console.log("new: " + newVal + "  oldVal: " + oldVal);
      this.$emit("setfilterto", newVal);
    },
  },
  mounted() {},
};
</script>

<style scoped>
</style>