<template>
    <main>
        <div class="title-container">
            <h2>Questionnaire</h2>
        </div>
        <div class="wrapper">
            <nav class="form-nav">
                <ul>
                    <li :class="{ active: activeForm === 'lifeJackets' }" @click="activeForm = 'lifeJackets'">
                        Gilets de sauvetage
                    </li>
                    <li :class="{ active: activeForm === 'safetyStances' }" @click="activeForm = 'safetyStances'">
                        Positions de sécurité</li>
                    <li :class="{ active: activeForm === 'emergencySlides' }" @click="activeForm = 'emergencySlides'">
                        Toboggans</li>
                    <li :class="{ active: activeForm === 'emergencyRafts' }" @click="activeForm = 'emergencyRafts'">
                        Canots de sauvetage
                    </li>
                    <li :class="{ active: activeForm === 'evacuation' }" @click="activeForm = 'evacuation'">
                        Evacuations
                    </li>
                    <li :class="{ active: activeForm === 'emergencyBeacons' }" @click="activeForm = 'emergencyBeacons'">
                        Balises de détresses</li>
                    <li  :class="{ active: activeForm === 'emergencyTools' }" @click="activeForm = 'emergencyTools'">
                        Moyens signalisation</li>
                    <li :class="{ active: activeForm === 'breathingHood' }" @click="activeForm = 'breathingHood'">
                        Cagoule de protection respiratoire</li>
                    <!-- Add more items later -->
                </ul>
            </nav>

            <div class="form-content">
                <LifeJacketsForm v-if="activeForm === 'lifeJackets'" />
                <SafetyStancesForm v-if="activeForm === 'safetyStances'" />
                <EmergencySlidesForm v-if="activeForm === 'emergencySlides'" />
                <EvacuationForm v-if="activeForm === 'evacuation'" />
                <EmergencyRaftsForm v-if="activeForm === 'emergencyRafts'" />
                <EmergencyBeaconsForm v-if="activeForm === 'emergencyBeacons'" />
                <EmergencyToolsForm v-if="activeForm === 'emergencyTools'" />
                <BreathingHoodForm v-if="activeForm === 'breathingHood'" />
                <!-- Add more forms here later -->
            </div>
        </div>
    </main>
</template>

<script>
import EmergencyRaftsForm from "./forms/EmergencyRaftsForm.vue";
import SafetyStancesForm from "./forms/SafetyStancesForm.vue";
import EmergencySlidesForm from "./forms/EmergencySlidesForm.vue";
import EvacuationForm from "./forms/EvacuationForm.vue";
import LifeJacketsForm from "./forms/LifeJacketsForm.vue";
import EmergencyBeaconsForm from "./forms/EmergencyBeaconsForm.vue";
import EmergencyToolsForm from "./forms/EmergencyToolsForm.vue";
import BreathingHoodForm from "./forms/BreathingHoodForm.vue"

export default {
    name: "FormComponent",
    components: {
        LifeJacketsForm,
        SafetyStancesForm,
        EmergencySlidesForm,
        EmergencyRaftsForm,
        EvacuationForm,
        EmergencyBeaconsForm,
        EmergencyToolsForm,
        BreathingHoodForm,
    },
    data() {
        return {
            activeForm: "lifeJackets", // default form
        };
    },
};
</script>

<style scoped lang="scss">
main {
    // display: grid;
    // grid-template-columns: 1fr;
    // grid-template-rows: 1fr;
    // border: 1px solid black;
    display: flex;
    flex-direction: column;

    .title-container {
        border: 1px solid black;
    }

    .wrapper {
        
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-template-rows: 1fr;

        .form-nav {
            display: flex;
            width: auto;
            max-width: 10vw;
            height: 100vh;

            ul {
                display: flex;
                flex-direction: column;
                list-style: none;
                gap: 1rem;
                padding: 0;
                width: auto;
                max-width: 90%;
                height: 100%;

                li {
                    cursor: pointer;
                    padding: 0.5rem 1rem;
                    border-bottom: 2px solid transparent;
                    &.active {
                        font-weight: bold;
                        // color: blue;
                    }
                }

            }
        }

        .form-content {
            margin-top: 2rem;
        }
    }
}
</style>
