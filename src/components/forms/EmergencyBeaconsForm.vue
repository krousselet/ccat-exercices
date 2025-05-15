<template>
  <form @submit.prevent="submitForm">
    <div v-for="(question, index) in questions" :key="index" class="block moveFromRight appear">
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
    <p v-if="score !== null" :class="{ danger: score < 3, success: score >= this.questions.length - 2 }">
      Votre score : {{ score }} / {{ questions.length }}
    </p>
  </form>
</template>
  
<script>
import confetti from "canvas-confetti";

export default {
  name: "EmergencyBeaconsForm",
  data() {
    return {
      formData: {
        emergencyBeaconsName: "",
        emergencyBeaconsFrequencyCount: "",
        emergencyBeaconsBeforeUse: "",
        emergencyBeaconsFrequencyDetails: "",
        emergencyBeaconsFrequencyType: "",
        emergencyBeaconsEmissionTime: "",
        emergencyBeaconsEmissionTimeAlteration: "",
        emergencyBeaconsPartsCount: "",
        emergencyBeaconsPartsName: "",
        emergencyBeaconsWaterSteps: "",
        emergencyBeaconsWaterStepsDetails: "",
      },
      score: null,
      audio: null,
      questions: [
        {
          text: "La balise de détresse a pour dénomination :",
          model: "emergencyBeaconsName",
          correct: "true",
          options: [
            { id: "emergencyBeaconsNameFalseOne", value: "false", label: "AET 406S" },
            { id: "emergencyBeaconsNameFalseTwo", value: "false", label: "EDT 405E" },
            { id: "emergencyBeaconsNameTrue", value: "true", label: "ADT 406S" },
            { id: "emergencyBeaconsNameFalseThree", value: "false", label: "MDT 406Y" },
          ],
        },
        {
          text: "La balise de détresse émet :",
          model: "emergencyBeaconsFrequencyCount",
          correct: "true",
          options: [
            { id: "emergencyBeaconsFrequencyCountFalseOne", value: "false", label: "Sur deux fréquences, la troisième requiert une manipulation" },
            { id: "emergencyBeaconsFrequencyCountTrue", value: "true", label: "Sur trois fréquences simultanément" },
            { id: "emergencyBeaconsFrequencyCountFalseTwo", value: "false", label: "Sur quatre fréquences simultanément" },
            { id: "emergencyBeaconsFrequencyCountFalseThree", value: "false", label: "Sur deux fréquences simultanément" },
          ],
        },
        {
          text: "Les fréquences d'emission sont :",
          model: "emergencyBeaconsFrequencyDetails",
          correct: "true",
          options: [
            { id: "emergencyBeaconsFrequencyDetailsFalseOne", value: "false", label: "406MHz, 125MHz, 250MHz" },
            { id: "emergencyBeaconsFrequencyDetailsTrue", value: "true", label: "406MHz, 121,5MHz, 243MHz" },
            { id: "emergencyBeaconsFrequencyDetailsFalseTwo", value: "false", label: "408MHz, 121,5MHz, 243MHz" },
            { id: "emergencyBeaconsFrequencyDetailsFalseThree", value: "false", label: "408MHz, 111,5MHz, 223MHz" },
          ],
        },
        {
          text: "Dans cette ordre (haute fréquence, fréquence moyenne, basse fréquence), la nature des émissions sont respectivement :",
          model: "emergencyBeaconsFrequencyType",
          correct: "true",
          options: [
            { id: "emergencyBeaconsFrequencyTypeFalse", value: "false", label: "Militaire, Satellitaire, civile" },
            { id: "emergencyBeaconsFrequencyTypeFalseOne", value: "false", label: "Civile, militaire, satellitaire" },
            { id: "emergencyBeaconsFrequencyTypeFalseTwo", value: "false", label: "Militaire, civile, militaire" },
            { id: "emergencyBeaconsFrequencyTypeTrue", value: "true", label: "Satellitaire, militaire, civile" },
          ],
        },
        {
          text: "La durée d'émission par fréquence (haute fréquence, fréquence moyenne, basse fréquence) est respectivement de :",
          model: "emergencyBeaconsEmissionTime",
          correct: "true",
          options: [
            { id: "emergencyBeaconsEmissionTimeTrue", value: "true", label: "24h, 48 | 60h, 48h | 60h" },
            { id: "emergencyBeaconsEmissionTimeFalse", value: "false", label: "48h, 24h | 48h, 24h | 33h" },
            { id: "emergencyBeaconsEmissionTimeFalseOne", value: "false", label: "33h, 48 | 60h, 48h | 60h" },
            { id: "emergencyBeaconsEmissionTimeFalseTwo", value: "false", label: "24h, 48h, 48h" },
          ],
        },
        {
          text: "La durée d'émission de la balise de détresse peut être affectée par :",
          model: "emergencyBeaconsEmissionTimeAlteration",
          correct: "true",
          options: [
            { id: "emergencyBeaconsEmissionTimeAlterationFalse", value: "false", label: "La salinité de l'eau, l'humidité de l'air, l'ensoleillement" },
            { id: "emergencyBeaconsEmissionTimeAlterationTrue", value: "true", label: "Une température très haute ou très basse" },
            { id: "emergencyBeaconsEmissionTimeAlterationFalseOne", value: "false", label: "Elles sont faites pour résister à tout" },
            { id: "emergencyBeaconsEmissionTimeAlterationFalseTwo", value: "false", label: "Les chocs reçus, son niveau de charge, le milieu ambiant" },
          ],
        },
        {
          text: "La balise de détresse est composée de :",
          model: "emergencyBeaconsPartsCount",
          correct: "true",
          options: [
            { id: "emergencyBeaconsPartsCount5", value: "false", label: "5 parties" },
            { id: "emergencyBeaconsPartsCount6", value: "false", label: "6 parties" },
            { id: "emergencyBeaconsPartsCount8", value: "false", label: "8 parties" },
            { id: "emergencyBeaconsPartsCountTrue", value: "true", label: "7 parties" },
          ],
        },
        {
          text: "Ces parties comptent entre autre :",
          model: "emergencyBeaconsPartsName",
          correct: "true",
          options: [
            {
              id: "emergencyBeaconsPartsNameFalse",
              value: "false",
              label: "Un corps ovoïde jaune, des arceaux de transport, des indicateurs visuels et sonores",
            },
            {
              id: "emergencyBeaconsPartsNameFalseOne",
              value: "false",
              label: "Une batterie lithium, un flotteur, un corps ovoïde orange",
            },
            {
              id: "emergencyBeaconsPartsNameTrue",
              value: "true",
              label: "1 capteur hydro sensible, une cordelette de retenue, un bouton TEST",
            },
            {
              id: "emergencyBeaconsPartsNameFalseTwo",
              value: "false",
              label: "2 capteurs hydro sensibles, un flotteur, une antenne et son embase",
            },
          ],
        },
        {
          text: "Pour une utilisation maritime, on se conforme à :",
          model: "emergencyBeaconsWaterSteps",
          correct: "true",
          options: [
            {
              id: "emergencyBeaconsWaterSteps3",
              value: "true",
              label: "3 étapes",
            },
            {
              id: "emergencyBeaconsWaterSteps2",
              value: "false",
              label: "2 étapes",
            },
            {
              id: "emergencyBeaconsWaterSteps1",
              value: "true",
              label: "Une seule étape",
            },
            {
              id: "emergencyBeaconsWaterSteps4",
              value: "false",
              label: "4 étapes",
            },
          ],
        },
        {
          text: "Pour une utilisation maritime, l'ordre de ces étapes est :",
          model: "emergencyBeaconsWaterStepsDetails",
          correct: "true",
          options: [
            {
              id: "emergencyBeaconsWaterStepsDetailsFalse",
              value: "false",
              label: "Préparation balise, pré-test, attente 30s, émission",
            },
            {
              id: "emergencyBeaconsWaterStepsDetailsFalseOne",
              value: "false",
              label: "pré-test, attente 45s, émission",
            },
            {
              id: "emergencyBeaconsWaterStepsDetailsFalseOne",
              value: "false",
              label: "Préparation balise, attente 30s, pré-test, émission",
            },
            {
              id: "emergencyBeaconsWaterStepsDetailsTrue",
              value: "true",
              label: "Préparation balise, attente 30s, émission",
            },
          ],
        },
        {
          text: "Pour une utilisation maritime, ces étapes sont :",
          model: "emergencyBeaconsWaterStepsOrder",
          correct: "true",
          options: [
            {
              id: "emergencyBeaconsWaterStepsOrderFalse",
              value: "false",
              label: "Fixer la balise au radeau, visser antenne ambase, position ARMED, mettre à l'eau la balise",
            },
            {
              id: "emergencyBeaconsWaterStepsOrderTrue",
              value: "true",
              label: "Visser antenne ambase, fixer la balise au radeau, position ARMED, mettre à l'eau la balise",
            },
            {
              id: "emergencyBeaconsWaterStepsOrderFalseOne",
              value: "false",
              label: "Visser antenne ambase, fixer la balise au radeau, position ON, mettre à l'eau la balise",
            },
            {
              id: "emergencyBeaconsWaterStepsOrderFalseTwo",
              value: "false",
              label: "Visser antenne ambase, position ARMED, fixer la balise au radeau, mettre à l'eau la balise",
            },
          ],
        },
        {
          text: "Pour une utilisation terrestre, on se conforme à :",
          model: "emergencyBeaconsGroundSteps",
          correct: "true",
          options: [
            {
              id: "emergencyBeaconsGroundSteps3",
              value: "false",
              label: "3 étapes",
            },
            {
              id: "emergencyBeaconsGroundSteps",
              value: "false",
              label: "2 étapes",
            },
            {
              id: "emergencyBeaconsGroundSteps1",
              value: "false",
              label: "Une seule étape",
            },
            {
              id: "emergencyBeaconsWaterSteps4",
              value: "true",
              label: "4 étapes",
            },
          ],
        },
        {
          text: "Pour une utilisation terrestre, l'ordre de ces étapes est :",
          model: "emergencyBeaconsWaterStepsDetailsGround",
          correct: "true",
          options: [
            {
              id: "emergencyBeaconsWaterStepsDetailsGroundFalse",
              value: "false",
              label: "",
            },
            {
              id: "emergencyBeaconsWaterStepsDetailsGroundFalseOne",
              value: "false",
              label: "",
            },
            {
              id: "emergencyBeaconsWaterStepsDetailsGroundFalseOne",
              value: "false",
              label: "",
            },
            {
              id: "emergencyBeaconsWaterStepsDetailsGroundTrue",
              value: "false",
              label: "",
            },
          ],
        },
        {
          text: "Pour une utilisation terrestre, ces étapes sont :",
          model: "emergencyBeaconsWaterStepsOrderGround",
          correct: "true",
          options: [
            {
              id: "emergencyBeaconsWaterStepsOrderGroundFalse",
              value: "false",
              label: "",
            },
            {
              id: "emergencyBeaconsWaterStepsOrderGroundFalseOne",
              value: "true",
              label: "",
            },
            {
              id: "emergencyBeaconsWaterStepsOrderGroundTrue",
              value: "false",
              label: "",
            },
            {
              id: "emergencyBeaconsWaterStepsOrderGroundFalseTwo",
              value: "false",
              label: "",
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

      if (score >= this.questions.length - 2) {
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
  form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  </style>
  