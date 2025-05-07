<template>
    <div class="wrapper">
      <form @submit.prevent="submitForm">
        <!-- Question 1 -->
        <div class="block">
          <label>Vide</label>
          <div class="together">
            <div class="group">
              <input
                type="radio"
                id="6"
                name="jacketsTypesCount"
                value="6"
                v-model="jacketsTypesCount"
              />
              <label for="6"></label>
            </div>
            <div class="group">
              <input
                type="radio"
                id="3"
                name="jacketsTypesCount"
                value="3"
                v-model="jacketsTypesCount"
              />
              <label for="3"></label>
            </div>
            <div class="group">
              <input
                type="radio"
                id="4"
                name="jacketsTypesCount"
                value="4"
                v-model="jacketsTypesCount"
              />
              <label for="4"></label>
            </div>
          </div>
        </div>
  
        <!-- Question 2 -->
        <div class="block">
          <label>Vide</label>
          <div class="together">
            <div class="group">
              <input
                type="radio"
                id="jacketsTypesTrue"
                name="jacketsTypes"
                value="true"
                v-model="jacketsTypes"
              />
              <label for="jacketsTypesTrue">Vrai</label>
            </div>
            <div class="group">
              <input
                type="radio"
                id="jacketsTypesFalse"
                name="jacketsTypes"
                value="false"
                v-model="jacketsTypes"
              />
              <label for="jacketsTypesFalse">Faux</label>
            </div>
          </div>
        </div>
  
        <!-- Question 3 -->
        <div class="block">
          <label
            >Vide</label
          >
          <div class="together">
            <div class="group">
              <input
                type="radio"
                id="jacketsCo2True"
                name="jacketsCo2"
                value="true"
                v-model="jacketsCo2"
              />
              <label for="jacketsCo2True">Vrai</label>
            </div>
            <div class="group">
              <input
                type="radio"
                id="jacketsCo2False"
                name="jacketsCo2"
                value="false"
                v-model="jacketsCo2"
              />
              <label for="jacketsCo2False">Faux</label>
            </div>
          </div>
        </div>
  
        <button type="submit">Envoyer</button>
        <p v-if="score !== null">Votre score : {{ score }} / {{ questionsCount }}</p>
      </form>
    </div>
  </template>
  
  <script>
  import confetti from "canvas-confetti";
  
  export default {
    name: "LifeJacketsForm",
    data() {
      return {
        jacketsTypesCount: "",
        jacketsTypes: "",
        jacketsCo2: "",
        score: null,
        audio: null,
        questionsCount: 1,
      };
    },
    mounted() {
      this.audio = new Audio('/sounds/cheers.mp3');
    },
    methods: {
      submitForm() {
        let score = 0;
  
        if (this.jacketsTypesCount === "3") score++;
        if (this.jacketsTypes === "false") score++;
        if (this.jacketsCo2 === "false") score++;
  
        this.score = score;
  
        if (score >= 3) {
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
  