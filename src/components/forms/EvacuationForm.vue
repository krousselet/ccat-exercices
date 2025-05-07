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
        <p v-if="score !== null">Votre score : {{ score }} / 3</p>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'EvacuationForm',
    data() {
      return {
        raftsCount: 0,
        inspectionDate: '',
      };
    },
    methods: {
      submitForm() {
        console.log('Submitted:', this.raftsCount, this.inspectionDate);
        // You can emit this data to the parent or save it elsewhere
      },
    },
  }
  </script>
  
  <style scoped>
  form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  </style>
  