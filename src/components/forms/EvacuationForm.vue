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
  name: "EvacuationForm",
  data() {
    return {
      formData: {
        evacuationPartsCount: "",
        evacuationHowToInflate: "",
        evacuationStepsEmbark: "",
        evacuationAlternativeMeans: "",
        evacuationAlwaysOnboard: "",
        evacuationComposition: "",
        evacuationVenturi: "",
      },
      score: null,
      audio: null,
      questions: [
        {
          text: "Sur un canot de sauvetages il y a :",
          model: "raftsPartsCount",
          correct: "true",
          options: [
            { id: "raftsPartsCountTrue", value: "true", label: "7 parties" },
            { id: "raftsPartsCountFalse", value: "false", label: "5 parties" },
            { id: "raftsPartsCountFalseOne", value: "false", label: "8 parties" },
            { id: "raftsPartsCountFalseTrue", value: "false", label: "6 parties" },
          ],
        },
        {
          text: "Les canots de secours se gonflent :",
          model: "raftsHowToInflate",
          correct: "true",
          options: [
            {
              id: "raftsHowToInflateBlowing",
              value: "false",
              label: "Les passagers se relaient pour gonfler à la bouche",
            },
            {
              id: "raftsHowToInflateSafetySlide",
              value: "false",
              label: "En provoquant l'armement du toboggan, l'air se transfert de celui-ci vers le canot",
            },
            {
              id: "raftsHowToInflateTrue",
              value: "true",
              label: "En deux temps, avec une cartouche de Co2 puis par un système d'aspiration",
            },
            {
              id: "raftsHowToInflateTrue",
              value: "false",
              label: "Le canot se gongle à l'aide d'une pompe à main",
            },
          ],
        },
        {
          text: "Combien d'étapes sont nécessaires avant d'embarquer dans un canot ?",
          model: "raftsStepsEmbark",
          correct: "true",
          options: [
            { id: "raftsStepsEmbark4", value: "false", label: "4" },
            { id: "raftsStepsEmbark7", value: "false", label: "7" },
            { id: "raftsStepsEmbark5", value: "false", label: "5" },
            { id: "raftsStepsEmbarkTrue", value: "true", label: "6" },
          ],
        },
        {
          text: "Si le canot ne se gonfle pas :",
          model: "raftsAlternativeMeans",
          correct: "true",
          options: [
            {
              id: "raftsAlternativeMeansBlow",
              value: "false",
              label: "On demande au pax requis de le gonfler avec la pompe à main",
            },
            {
              id: "raftsAlternativeMeansAnyway",
              value: "false",
              label: "On embarque quand même, car mieux vaut un canot défaillant que rien",
            },
            {
              id: "raftsAlternativeMeans",
              value: "false",
              label: "On demande au pax requis de plonger activer le compresseur de secours sous le canot",
            },
            {
              id: "raftsAlternativeMeansTrue",
              value: "true",
              label: "On redirige les personnes vers un canot fonctionnel",
            },
          ],
        },
        {
          text: "On embarque tout le temps les canots de sauvetage",
          model: "raftsAlwaysOnboard",
          correct: "true",
          options: [
            {
              id: "raftsAlwaysOnboardDesert",
              value: "false",
              label: "Oui, car on peut s'en servir contre le soleil dans le désert",
            },
            {
              id: "raftsAlwaysOnboardTrue",
              value: "true",
              label: "Non, seulement en survol maritime",
            },
            {
              id: "raftsAlwaysOnboardSnow",
              value: "false",
              label: "Oui, car on peut en faire des igloos en les isolant avec de la neige",
            },
            {
              id: "raftsAlwaysOnboardPlace",
              value: "false",
              label: "Non, cela dépend du nombre de passagers emportés",
            },
          ],
        },
        {
          text: "Un canot de sauvetage est composé :",
          model: "raftsComposition",
          correct: "true",
          options: [
            {
              id: "raftsCompositionTrue",
              value: "true",
              label: "2 saisines, deux tores superposés, un toit, une balise lumineuse",
            },
            {
              id: "raftsCompositionFalse",
              value: "false",
              label: "1 saisine, 1 tore, une rigole de récupération, des stabilisateurs",
            },
            {
              id: "raftsCompositionFalseOne",
              value: "false",
              label: "1 saisine, deux tores superposés, une échelle, une balise lumineuse",
            },
            {
              id: "raftsCompositionFalseTwo",
              value: "false",
              label: "Une voile, 2 tores superposés, 2 saisines, une échelle",
            },
          ],
        },
         {
          text: "Les valves sur les canots sont :",
          model: "raftsVenturi",
          correct: "true",
          options: [
            {
              id: "raftsPenturi",
              value: "false",
              label: "Les valves penturi",
            },
            {
              id: "raftsCentury",
              value: "false",
              label: "Les valves century",
            },
            {
              id: "raftsVenturi",
              value: "true",
              label: "Les valves venturi",
            },
            {
              id: "raftsBenturi",
              value: "false",
              label: "Les valves benturi",
            },
          ],
        },
        {
          text: "Ces valves permettent de :",
          model: "raftsVenturiGoal",
          correct: "true",
          options: [
            {
              id: "raftsVenturiGoalAnchor",
              value: "false",
              label: "Maintenir les canots fixés à l'avion pour éviter la dérive",
            },
            {
              id: "raftsVenturiWater",
              value: "false",
              label: "Stocker de l'eau dans les tores plutôt que de l'air",
            },
            {
              id: "raftsVenturiWeight",
              value: "false",
              label: "Prévenir l'explosion des tores en cas de surnombre sur les canots",
            },
            {
              id: "raftsVenturiTrue",
              value: "true",
              label: "Complètent le gonflage de la cartouche Co2",
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
  