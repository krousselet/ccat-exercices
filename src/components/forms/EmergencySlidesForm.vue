<template>
  <form @submit.prevent="submitForm">
    <div v-for="(question, index) in questions" :key="index" class="block moveFromRight appear">
      <p class="question">{{ `${index + 1}) ${question.text}`  }}</p>
          <div class="together" :class="{ danger: submitted && formData[question.model] !== question.correct }">
        <div v-for="(option, idx) in question.options" :key="idx" class="group">
          <input
            type="radio"
            :id="option.id"
            :name="question.model"
            :value="option.value"
            :class="{danger: option.value === false}"
            v-model="formData[question.model]"
          />
          <label :for="option.id">{{ option.label }}</label>
        </div>
      </div>
    </div>
    <!-- Submit and Score -->
    <button type="submit">Envoyer</button>
    <p v-if="score !== null" :class="{ danger: score < 6, success: score >= 6 }">
      Votre score : {{ score }} / {{ questions.length }}
    </p>
  </form>
</template>

<script>
import confetti from "canvas-confetti";

export default {
  name: "EmergencySlidesForm",
  data() {
    return {
      formData: {
        emergencyExitTypes: "",
        howToJump: "",
        paxPosition: "",
        paxRole: "",
        convertibleSlidesBasics: "",
        armingEmergencySlides: "",
        emergencySlidesSteps: "",
        paxMissionWater: "",
      },
      score: null,
      audio: null,
      submitted: false,
      questions: [
        {
          text: "Il n'existe que trois types d'issues de secours",
          model: "emergencyExitTypes",
          correct: "true",
          options: [
            { id: "emergencyExitTypesFalse", value: "false", label: "Vrai" },
            { id: "emergencyExitTypesTrue", value: "true", label: "Faux" },
          ],
        },
        {
          text: "Sur un toboggan non-convertible, on saute :",
          model: "howToJump",
          correct: "true",
          options: [
            {
              id: "howToJumpSteward",
              value: "false",
              label: "Dos au vide pour garder un oeil sur les instructions",
            },
            {
              id: "howToJumpKnees",
              value: "false",
              label: "Les genoux entourés par les bras",
            },
            {
              id: "howToJumpTrue",
              value: "true",
              label: "Bras et jambes tendus",
            },
            {
              id: "howToJumpNeck",
              value: "false",
              label: "Les mains contre la nuque pour palier un coup du lapin",
            },
          ],
        },
        {
          text: "Le PAX est au point de commandement (en haut du toboggan)",
          model: "paxPosition",
          correct: "true",
          options: [
            { id: "paxPositionFalse", value: "false", label: "Vrai" },
            { id: "paxPositionTrue", value: "true", label: "Faux" },
          ],
        },
        {
          text: "Le PAX requis a pour rôle :",
          model: "paxRole",
          correct: "true",
          options: [
            {
              id: "paxRoleTrue",
              value: "true",
              label: "D'assister les personnes à s'éloigner de l'avion",
            },
            {
              id: "paxRoleHurt",
              value: "false",
              label: "De maîtriser par la force les contrevenants",
            },
            {
              id: "paxRoleCount",
              value: "false",
              label: "De compter les personnes évacuées pour remplir les quotas",
            },
            {
              id: "paxRoleguardian",
              value: "false",
              label: "De surveiller qu'aucun incendie ne survienne pendant l'évacuation",
            },
          ],
        },
        {
          text: "Le toboggan réversible est équipé :",
          model: "convertibleSlidesBasics",
          correct: "true",
          options: [
            {
              id: "convertibleSlidesBasicsFalse",
              value: "false",
              label: "Mâts, voiles, container survie, 2 tores superposés",
            },
            {
              id: "convertibleSlidesBasicsFalseTwo",
              value: "false",
              label: "Filets, rames, container survie, 2 tores superposés",
            },
            {
              id: "convertibleSlidesBasicsTrue",
              value: "true",
              label: "Mâts, container survie, 2 tores superposés",
            },
            {
              id: "convertibleSlidesBasicsFalseThree",
              value: "false",
              label: "Mâts, container survie, 3 tores superposés",
            },
          ],
        },
        {
          text: "On vérifie l'armement des toboggans :",
          model: "armingEmergencySlides",
          correct: "true",
          options: [
            {
              id: "armingEmergencySlidesCaptain",
              value: "false",
              label: "Sur ordre du commandant",
            },
            {
              id: "armingEmergencySlidesControl",
              value: "false",
              label: "Après l'accord tour de contrôle",
            },
            {
              id: "armingEmergencySlidesEnginesOn",
              value: "true",
              label: "Lors du démarrage des moteurs",
            },
            {
              id: "armingEmergencySlidesMyself",
              value: "false",
              label: "Le PNC le fait à son initiative",
            },
          ],
        },
        {
          text: "Quelles sont les étapes à réaliser avant une évacuation ?",
          model: "emergencySlidesSteps",
          correct: "true",
          options: [
            {
              id: "emergencySlidesStepsTrue",
              value: "true",
              label: "Vérifier l'armement, vérifier le gonflage, activer gonflage secours, rediriger",
            },
            {
              id: "emergencySlidesStepsFalse",
              value: "false",
              label: "Désarmer le toboggan, vérifier les environs, ouvrir la porte et évacuer",
            },
            {
              id: "emergencySlidesStepsFalseOne",
              value: "false",
              label: "Désarmer le toboggan, vérifier le gonflage, activer gonflage secours, rediriger",
            },
            {
              id: "emergencySlidesStepsFalseTwo",
              value: "false",
              label: "Vérifier l'armement, vérifier le gonflage, activer gonflage secours, évacuer quoi qu'il en coûte",
            },
          ],
        },
         {
          text: "En survie maritime, le PAX doit :",
          model: "paxMissionWater",
          correct: "true",
          options: [
            { id: "paxMissionWaterFalse", value: "false", label: "Prévenir les chutes du toboggan, organiser l'espace sur le toboggan, rassurer" },
            { id: "paxMissionWaterTrue", value: "true", label: "Tentre la sangle de sécurité, détacher le toboggan en activant le délaçage du filin" },
            { id: "paxMissionWaterFalseOne", value: "false", label: "En maritime, le PAX requis n'est pas différent d'un PAX lambda" },
            { id: "paxMissionWaterFalseTwo", value: "false", label: "Disposer des mêmes privilèges que le PNC car la survie en dépend" },
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
      this.submitted = true;
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
.danger {
  color: red;
  transition: 0.5s ease;
}

.success {
  color: green;
  transition: 0.5s ease;
}

label {
  display: inline;
  width: auto;
  height: auto;
  text-align: justify;
  min-width: 50px;
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

p {
  text-align: center;
  font-weight: bold;
}
</style>
