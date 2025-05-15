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
    <p v-if="score !== null" :class="{ danger: score < 2, success: score >= 2 }">
      Votre score : {{ score }} / {{ questions.length }}
    </p>
  </form>
</template>

<script>
import confetti from "canvas-confetti";

export default {
  name: "SafetyStancesForm",
  data() {
    return {
      formData: {
        stancesCriteria: "",
        stancesCount: "",
        stancesAlways: "",
      },
      score: null,
      audio: null,
      questions: [
        {
          text: "Combien de critères déterminent une position plutôt qu'une autre ?",
          model: "stancesCriteria",
          correct: "true",
          options: [
            { id: "stancesCriteria2", value: "false", label: "2" },
            { id: "stancesCriteriaTrue", value: "true", label: "3" },
            { id: "stancesCriteria4", value: "false", label: "4" },
            { id: "stancesCriteria5", value: "false", label: "5" },
          ],
        },
        {
          text: "Combien de positions existe-t-il ?",
          model: "stancesCount",
          correct: "true",
          options: [
            {
              id: "stancesCount2",
              value: "false",
              label: "2",
            },
            {
              id: "stancesCount3",
              value: "false",
              label: "3",
            },
             {
              id: "stancesCount5",
              value: "false",
              label: "5",
            },
             {
              id: "stancesCount4",
              value: "true",
              label: "4",
            },
          ],
        },
        {
          text: "Est commun à toutes les positions :",
          model: "stancesAlways",
          correct: "true",
          options: [
            { id: "stancesAlwaysFalse", value: "false", label: "Ceinture détachée pour faciliter l'évacuation" },
            { id: "stancesAlwaysFalseOne", value: "false", label: "Ceinture attachée et ajustée, pieds sur le siège faisant face" },
            { id: "stancesAlwaysTrue", value: "true", label: "Ceinture attachée et ajustée, pieds et genoux serrés" },
            { id: "stancesAlwaysFalseTwo", value: "false", label: "Mains derrière la nuque pour prévenir le coup du lapin" },
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
.danger {
  color: red;
  transition: .5s ease;
}

.success {
  color: green;
  transition: .5s ease;
}

p {
  text-align: center;
  font-weight: bold;
}
</style>
