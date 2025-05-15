<template>
  <nav>
    <router-link class="die-link" to="/">Home</router-link>
    <router-link class="die-link" to="/about">About</router-link>
    <router-link class="die-link" to="/forms">Questionnaires</router-link>
  </nav>
  <router-view/>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  // background:  linear-gradient(#103A65, #548BA3);
}

nav {
  padding: 30px;
  display: flex;
  justify-content: space-around;
  align-items: center;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: red;
    }
  }
}

button {
  transition: .5s;
  margin: 20px auto;
  padding: 10px 20px;
  outline: none;
  border: none;
  border-radius: 7px;
  box-shadow: 0 0 5px black;
  cursor: pointer;
  &:active {
    transition: .1s;
    transform: scale(.9);
    box-shadow: 0 0 15px black;
  }
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
  overflow-x: hidden;
}

.block {
  display: flex;
  flex-direction: column;
  gap: 25px;
  margin: 25px auto;
  height: 100%;
  position: relative;
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

.danger {
  color: red;
}

.success {
  color: green;
}

// ROLL TRANSITION
.die-link {
  display: inline-block;
  padding: 15px 15px;
  background: transparent;
  color: black;
  text-decoration: none;
  border-radius: 8px;
  perspective: 1000px; /* enables 3D */
  transition: 0.6s ease-in-out;
  transform-style: preserve-3d;
  &:hover {
    transition: 0.3s ease-in-out;
    background: #002157;
    color: white;
    transform: rotateX(360deg);
  }
}

.appear {
  opacity: 1;
  animation: appear .3s .2s ease-in-out forwards;
}

.moveFromLeft {
  left: -25vw;
  animation: moveFromLeft .3s .2s ease-in-out forwards;
}

.moveFromRight {
  right: -50vw;
  animation: moveFromRight .3s .2s ease-in-out forwards;
}

//KEYFRAMES
@keyframes appear {
  100% {
    opacity: 1;
  }
}

@keyframes moveFromLeft {
  100% {
    left: 0;
  }
}

@keyframes moveFromRight {
  100% {
    right: 0;
  }
}

</style>
