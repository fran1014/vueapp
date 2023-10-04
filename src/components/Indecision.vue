<template>
  <div>
    <img :src="img" alt="bg" />
    <div class="bg-dark"></div>

    <div class="indecision-container">
      <input v-model="question" type="text" placeholder="hazme una pregunta" />
      <p>Remember to finish with an interrogation mark (?)</p>
      <div v-if="isValidQuestion">
        <h2>{{ question }}</h2>
        <h1>{{ answer }}</h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      question: null,
      answer: null,
      image: null,
      isValidQuestion: false,
    };
  },
  methods: {
    async getAnswer() {
      this.answer = 'Pensando....';

      const { answer, image } = await fetch('https://yesno.wtf/api').then((r) =>
        r.json()
      );

      this.answer = answer;
      this.img = image;
    },
  },
  watch: {
    question(value, oldValue) {
      this.isValidQuestion = false;

      if (!value.includes('?')) return;

      this.isValidQuestion = true;

      this.getAnswer();
    },
  },
};
</script>

<style>
img,
.bg-dark {
  height: 100vh;
  left: 0;
  max-height: 100%;
  max-width: 100%;
  position: fixed;
  top: 0px;
  width: 100vh;
}

.bg-dark {
  background-color: rgba(0, 0, 0, 0.4);
}

.indecision-container {
  position: relative;
  z-index: 99;
}

input {
  width: 250px;
  padding: 10px 15px;
  border-radius: 5px;
  border: none;
}

input:focus {
  outline: none;
}

p {
  color: #fff;
  font-size: 20px;
  margin-top: 0;
}

h1,
h2 {
  color: #fff;
}

h2 {
  margin-top: 150px;
}
</style>
