<template>
  <div>
    <h2>Counter</h2>

    <p>{{ counter }} <sup>2</sup> = {{ squareCounter }}</p>
    <button>+1</button>
    <button>-1</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      counter: 5,
    };
  },
  methods: {
    getSquareValue() {
      return this.counter * this.counter;
    },
  },
  computed: {
    squareCounter() {
      return this.counter * this.counter;
    },
  },
};
</script>

<style></style>
