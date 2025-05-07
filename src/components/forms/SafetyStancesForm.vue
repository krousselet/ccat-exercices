<template>
    <div class="wrapper">
      <form @submit.prevent="submitForm">
        <!-- Question 1 -->
        <div class="block">
          <label>Combien de positions existe-t-il ?</label>
          <div class="together">
            <div class="group">
              <input
                type="radio"
                id="2"
                name="stancesCount"
                value="2"
                v-model="stancesCount"
              />
              <label for="2">2</label>
            </div>
            <div class="group">
              <input
                type="radio"
                id="3"
                name="stancesCount"
                value="3"
                v-model="stancesCount"
              />
              <label for="3">3</label>
            </div>
            <div class="group">
              <input
                type="radio"
                id="4"
                name="stancesCount"
                value="4"
                v-model="stancesCount"
              />
              <label for="4">4</label>
            </div>
          </div>
        </div>
        <button type="submit">Envoyer</button>
        <p v-if="score !== null">Votre score : {{ score }} / 3</p>
      </form>
    </div>
  </template>
  
  <script>
  import confetti from "canvas-confetti";
  
  export default {
    name: "SafetyStancesForm",
    data() {
      return {
        stancesCount: "",
        score: null,
        audio: null,
      };
    },
    mounted() {
      this.audio = new Audio('/sounds/cheers.mp3');
    },
    methods: {
      submitForm() {
        let score = 0;
  
        if (this.stancesCount === "4") score++;
        // if (this.jacketsTypes === "false") score++;
        // if (this.jacketsCo2 === "false") score++;
  
        this.score = score;
  
        if (score === 1) {
          // Play sound
          this.audio.play();
  
          // Launch confetti
          confetti({
            particleCount: 100,
            spread: 70,
            origin: { y: 0.6 },
          });
        }
  
        console.log("Score:", score + "/3");
      },
    },
  };
  </script>
  
  <style scoped>
  .wrapper {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr;
  }
  
  form {
    display: flex;
    flex-direction: column;
  }
  
  .block {
    display: flex;
    flex-direction: column;
    gap: 25px;
    margin: 25px auto;
  }
  
  .together {
    display: flex;
    justify-content: space-around;
  }
  
  button {
    margin: 20px auto;
    padding: 10px 20px;
  }
  
  p {
    text-align: center;
    font-weight: bold;
    color: green;
  }
  </style>
  