<template>
  <div class="wrapper">
    <form @submit.prevent="submitForm">
      <!-- Question 1 -->
      <div class="block">
        <p class="question">Combien de types de gilets utilise-t-on ?</p>
        <div class="together">
          <div class="group" v-for="n in [6, 3, 4, 1]" :key="n">
            <input
              :id="'jacketsTypesCount' + n"
              type="radio"
              name="jacketsTypesCount"
              :value="n.toString()"
              v-model="jacketsTypesCount"
            />
            <label :for="'jacketsTypesCount' + n">{{ n }}</label>
          </div>
        </div>
      </div>

      <!-- Question 2 -->
      <div class="block">
        <p class="question">Il existe un seul type de gilet double chambre réversible</p>
        <div class="together">
          <div class="group">
            <input id="jacketsTypesTrue" type="radio" name="jacketsTypes" value="true" v-model="jacketsTypes" />
            <label for="jacketsTypesTrue">Vrai</label>
          </div>
          <div class="group">
            <input id="jacketsTypesFalse" type="radio" name="jacketsTypes" value="false" v-model="jacketsTypes" />
            <label for="jacketsTypesFalse">Faux</label>
          </div>
        </div>
      </div>

      <!-- Question 3 -->
      <div class="block">
        <p class="question">Sur le gilet non-réversible on place la cartouche de CO2 devant</p>
        <div class="together">
          <div class="group">
            <input id="jacketsCo2True" type="radio" name="jacketsCo2" value="true" v-model="jacketsCo2" />
            <label for="jacketsCo2True">Vrai</label>
          </div>
          <div class="group">
            <input id="jacketsCo2False" type="radio" name="jacketsCo2" value="false" v-model="jacketsCo2" />
            <label for="jacketsCo2False">Faux</label>
          </div>
        </div>
      </div>

      <!-- Question 4 -->
      <div class="block">
        <p class="question">Dans quel milieu utilise-t-on les gilets de sauvetage ?</p>
        <div class="together">
          <div class="group">
            <input id="jacketsUseLand" type="radio" name="jacketsUse" value="land" v-model="jacketsUse" />
            <label for="jacketsUseLand">Terrestre</label>
          </div>
          <div class="group">
            <input id="jacketsUseMaritime" type="radio" name="jacketsUse" value="true" v-model="jacketsUse" />
            <label for="jacketsUseMaritime">Maritime</label>
          </div>
          <div class="group">
            <input id="jacketsUseAll" type="radio" name="jacketsUse" value="all" v-model="jacketsUse" />
            <label for="jacketsUseAll">Tout milieu</label>
          </div>
          <div class="group">
            <input id="jacketsUseDay" type="radio" name="jacketsUse" value="day" v-model="jacketsUse" />
            <label for="jacketsUseDay">Seulement de jour</label>
          </div>
        </div>
      </div>

      <!-- Question 5 -->
      <div class="block">
        <p class="question">Un gilet à double chambre présente un seul embout buccal pour les deux chambres</p>
        <div class="together">
          <div class="group">
            <input id="jacketsBlowFalse1" type="radio" name="jacketsBlow" value="true" v-model="jacketsBlow" />
            <label for="jacketsBlowFalse1">Faux</label>
          </div>
          <div class="group">
            <input id="jacketsBlowTrue" type="radio" name="jacketsBlow" value="false" v-model="jacketsBlow" />
            <label for="jacketsBlowTrue">Vrai</label>
          </div>
          <div class="group">
            <input id="jacketsBlowChildren" type="radio" name="jacketsBlow" value="children" v-model="jacketsBlow" />
            <label for="jacketsBlowChildren">Gilets enfants uniquement</label>
          </div>
          <div class="group">
            <input id="jacketsBlowManex" type="radio" name="jacketsBlow" value="manex" v-model="jacketsBlow" />
            <label for="jacketsBlowManex">Voir Manex</label>
          </div>
        </div>
      </div>

      <!-- Question 6 -->
      <div class="block">
        <p class="question">La balise lumineuse doit avoir une durée de vie de :</p>
        <div class="together">
          <div class="group">
            <input id="lightBeacon6h" type="radio" name="lightBeacon" value="6" v-model="lightBeacon" />
            <label for="lightBeacon6h">6h</label>
          </div>
          <div class="group">
            <input id="lightBeacon12h" type="radio" name="lightBeacon" value="12" v-model="lightBeacon" />
            <label for="lightBeacon12h">12h</label>
          </div>
          <div class="group">
            <input id="lightBeaconUnlimited" type="radio" name="lightBeacon" value="unlimited" v-model="lightBeacon" />
            <label for="lightBeaconUnlimited">Illimitée</label>
          </div>
          <div class="group">
            <input id="lightBeacon24h" type="radio" name="lightBeacon" value="true" v-model="lightBeacon" />
            <label for="lightBeacon24h">24h</label>
          </div>
        </div>
      </div>

      <!-- Question 7 -->
      <div class="block">
        <p class="question">Les gilets à double chambre doivent se composer de :</p>
        <div class="together">
          <div class="group">
            <input id="jacketsComp1" type="radio" name="jacketsComposition" value="opt1" v-model="jacketsComposition" />
            <label for="jacketsComp1">2 systèmes de percussion<br />2 embouts buccaux<br />1 cartouche de CO2</label>
          </div>
          <div class="group">
            <input id="jacketsComp2" type="radio" name="jacketsComposition" value="opt2" v-model="jacketsComposition" />
            <label for="jacketsComp2">1 système de percussion<br />2 embouts buccaux<br />2 cartouches de CO2</label>
          </div>
          <div class="group">
            <input id="jacketsComp3" type="radio" name="jacketsComposition" value="true" v-model="jacketsComposition" />
            <label for="jacketsComp3">2 systèmes de percussion<br />2 embouts buccaux<br />2 cartouches de CO2</label>
          </div>
          <div class="group">
            <input id="jacketsComp4" type="radio" name="jacketsComposition" value="opt4" v-model="jacketsComposition" />
            <label for="jacketsComp4">2 systèmes de percussion<br />1 embout buccal<br />2 cartouches de CO2</label>
          </div>
        </div>
      </div>

      <!-- Question 8 -->
      <div class="block">
        <p class="question">Tous les gilets ont un système de gonflage automatique</p>
        <div class="together">
          <div class="group">
            <input id="jacketsAutoBlowTrue" type="radio" name="jacketsAutoBlow" value="true" v-model="jacketsAutoBlow" />
            <label for="jacketsAutoBlowTrue">Faux</label>
          </div>
          <div class="group">
            <input id="jacketsAutoBlowFalse" type="radio" name="jacketsAutoBlow" value="false" v-model="jacketsAutoBlow" />
            <label for="jacketsAutoBlowFalse">Vrai</label>
          </div>
          <div class="group">
            <input id="jacketsAutoMono" type="radio" name="jacketsAutoBlow" value="mono" v-model="jacketsAutoBlow" />
            <label for="jacketsAutoMono">Mono uniquement</label>
          </div>
          <div class="group">
            <input id="jacketsAutoReversible" type="radio" name="jacketsAutoBlow" value="reversible" v-model="jacketsAutoBlow" />
            <label for="jacketsAutoReversible">Réversibles uniquement</label>
          </div>
        </div>
      </div>

      <!-- Submit + Result -->
      <button type="submit">Envoyer</button>
      <p v-if="score !== null" :class="{ 'danger': score < 6 }">
        Votre score : {{ score }} / {{ questionsNumber }}
      </p>
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
      jacketsUse: "",
      jacketsBlow: "",
      lightBeacon: "",
      jacketsComposition: "",
      jacketsAutoBlow: "",
      score: null,
      audio: null,
      questionsNumber: 20,
    };
  },
  mounted() {
    this.audio = new Audio("/sounds/cheers.mp3");
  },
  methods: {
    submitForm() {
      let score = 0;

      if (this.jacketsTypesCount === "3") score++;
      if (this.jacketsTypes === "false") score++;
      if (this.jacketsCo2 === "false") score++;
      if (this.jacketsUse === "true") score++;
      if (this.jacketsBlow === "true") score++;
      if (this.lightBeacon === "true") score++;
      if (this.jacketsComposition === "true") score++;
      if (this.jacketsAutoBlow === "true") score++;

      this.score = score;

      if (score >= 15) {
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
.danger {
  color: red;
}

.wrapper {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr;
  width: 100%;
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
  height: 100%;
}

.together {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 25px;
  height: 100%;
}

.question {
  font-weight: bold;
}

button {
  margin: 20px auto;
  padding: 10px 20px;
}

p {
  text-align: center;
  font-weight: bold;
}
</style>
