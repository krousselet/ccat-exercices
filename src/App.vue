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

</style>
