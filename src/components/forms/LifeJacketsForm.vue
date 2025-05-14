<template>
  <form @submit.prevent="submitForm">
    <div v-for="(question, index) in questions" :key="index" class="block">
      <p class="question">{{ `${index + 1}) ${question.text}`  }}</p>
      <div class="together">
        <div v-for="(option, idx) in question.options" :key="idx" class="group">
          <input
            type="radio"
            :id="option.id"
            :name="question.model"
            :value="option.value"
            v-model="formData[question.model]"
          />
          <label :for="option.id">{{ option.label }}</label>
        </div>
      </div>
    </div>

    <!-- Submit and Score -->
    <button type="submit">Envoyer</button>
    <p v-if="score !== null" :class="{ danger: score < 7, success: score >= 8 }">
      Votre score : {{ score }} / {{ questions.length }}
    </p>
  </form>
</template>

<script>
import confetti from "canvas-confetti";

export default {
  name: "LifeJacketsForm",
  data() {
    return {
      formData: {
        emergencyExitTypes: "",
        howToJump: "",
        paxPosition: "",
        paxRole: "",
        convertibleSlidesBasics: "",
      },
      score: null,
      audio: null,
      questions: [
        {
          text: "Combien de types de gilets utilise-t-on ?",
          model: "jacketsTypesCount",
          correct: "true",
          options: [
            { id: "jacketsTypesCount6", value: "false", label: "6" },
            { id: "jacketsTypesCount3", value: "false", label: "3" },
            { id: "jacketsTypesCount1", value: "false", label: "1" },
            { id: "jacketsTypesCountTrue", value: "true", label: "4" },
          ],
        },
        {
          text: "Il existe un seul type de gilet double chambre réversible",
          model: "jacketsTypes",
          correct: "true",
          options: [
            {
              id: "jacketsTypesFalse",
              value: "false",
              label: "Vrai",
            },
            {
              id: "jacketsTypesTrue",
              value: "true",
              label: "Faux",
            },
          ],
        },
        {
          text: "Sur le gilet non-réversible on place la cartouche de CO2 devant",
          model: "jacketsCo2",
          correct: "true",
          options: [
            { id: "jacketsCo2False", value: "false", label: "Vrai" },
            { id: "jacketsCo2True", value: "true", label: "Faux" },
          ],
        },
        {
          text: "Dans quel milieu utilise-t-on les gilets de sauvetage ?",
          model: "jacketsUse",
          correct: "true",
          options: [
            {
              id: "jacketsUseTerrestre",
              value: "false",
              label: "Terrestre",
            },
            {
              id: "jacketsUseMaritime",
              value: "true",
              label: "Maritime",
            },
            {
              id: "jacketsUseAll",
              value: "false",
              label: "Tout milieu",
            },
            {
              id: "jacketsUseDay",
              value: "false",
              label: "Seulement de jour",
            },
          ],
        },
        {
          text: "Un gilet à double chambre présente un seul embout buccal pour les deux chambres",
          model: "jacketsBlow",
          correct: "true",
          options: [
            {
              id: "jacketsBlowTrue",
              value: "true",
              label: "Faux",
            },
            {
              id: "jacketsBlowFalse",
              value: "false",
              label: "Vrai",
            },
            {
              id: "jacketsBlowChildrenOnly",
              value: "false",
              label: "Gilets enfants uniquement",
            },
            {
              id: "jacketsBlowManex",
              value: "false",
              label: "Voir manex",
            },
          ],
        },
      {
          text: "La balise lumineuse doit avoir une durée de vie de :",
          model: "lightBeacon",
          correct: "true",
          options: [
            {
              id: "lightBeacon",
              value: "false",
              label: "6h",
            },
            {
              id: "lightBeaconInfinite",
              value: "false",
              label: "Illimitée",
            },
            {
              id: "lightBeaconTrue",
              value: "true",
              label: "24h",
            },
            {
              id: "lightBeaconTwelveHour",
              value: "false",
              label: "12h",
            },
          ],
        },
      {
          text: "Les gilets à double chambre doivent se composer de :",
          model: "jacketsComposition",
          correct: "true",
          options: [
            {
              id: "jacketsCompositionFalse",
              value: "false",
              label: "2 systèmes de percussion, 2 embouts buccaux, 1 cartouche de CO2",
            },
            {
              id: "jacketsCompositionTrue",
              value: "true",
              label: "2 systèmes de percussion, 2 embouts buccaux, 2 cartouches de CO2",
            },
            {
              id: "jacketsCompositionFalseOne",
              value: "false",
              label: "1 système de percussion, 2 embouts buccaux, 2 cartouches de CO2",
            },
            {
              id: "jacketsCompositionFalseTwo",
              value: "false",
              label: "2 systèmes de percussion, 1 embout buccal, 2 cartouches de CO2",
            },
          ],
        },
      {
          text: "Tous les gilets ont un système de gonflage automatique",
          model: "jacketsAutoBlow",
          correct: "true",
          options: [
            {
              id: "jacketsAutoBlowFalse",
              value: "false",
              label: "Vrai",
            },
            {
              id: "jacketsAutoBlowMono",
              value: "false",
              label: "Monos uniquement",
            },
            {
              id: "jacketsAutoBlowConvertible",
              value: "false",
              label: "Réversibles uniquement",
            },
            {
              id: "jacketsAutoBlowTrue",
              value: "true",
              label: "Faux",
            },
          ],
        },
      {
          text: "Les adultes doivent immédiatement gonfler leur gilet de sauvetage :",
          model: "jacketsWhenToBlow",
          correct: "true",
          options: [
            {
              id: "jacketsWhenToBlowTrue",
              value: "true",
              label: "Au seuil de la porte",
            },
            {
              id: "jacketsWhenToBlowCabine",
              value: "false",
              label: "Pendant la préparation cabine",
            },
            {
              id: "jacketsWhenToBlowCrash",
              value: "false",
              label: "Juste avant le crash",
            },
            {
              id: "jacketsWhenToBlowWater",
              value: "false",
              label: "Au contact de l'avion avec l'eau",
            },
          ],
        },
      {
          text: "De quoi dispose un gilet bébé que les autres n'ont pas ?",
          model: "jacketsBaby",
          correct: "true",
          options: [
            {
              id: "jacketsBabyStandard",
              value: "false",
              label: "Tous sont standards",
            },
            {
              id: "jacketsBabyStandardBottle",
              value: "false",
              label: "Un biberon",
            },
            {
              id: "jacketsBabyStandardCo2",
              value: "false",
              label: "Une cartouche de Co2 supplémentaire",
            },
            {
              id: "jacketsBabyStandardTrue",
              value: "true",
              label: "Une cordelette de retenue",
            },
          ],
        },
      ],
    };
  },
  mounted() {
    this.audio = new Audio("/sounds/cheers.mp3");
  },
  methods: {
    submitForm() {
      let score = 0;

      for (const question of this.questions) {
        if (this.formData[question.model] === question.correct) {
          score++;
        }
      }

      this.score = score;

      if (score >= 8) {
        this.audio.play();
        confetti({
          particleCount: 100,
          spread: 70,
          origin: { y: 0.6 },
        });
      }
    },
  },
};
</script>

<style scoped>
.danger {
  color: red;
  transition: .5s ease;
}

.success {
  color: green;
  transition: .5s ease;
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
