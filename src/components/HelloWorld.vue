<template>
  <main>
    <div class="image-container">
      <picture>
        <source media="(min-width:320px) and (max-width: 550px)" srcset="/images/mobile/plane.svg">
        <source media="(min-width: 551px)" srcset="/images/desktop/plane.svg">
        <img src="/images/desktop/plane.svg" alt="image de pncs" style="width:auto;">
      </picture>
    </div>
  </main>
</template>

<script>
export default {
  name: 'HelloWorld',
 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

@media (min-width:320px) and (max-width: 550px) {
  main {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr;

    picture {
      max-width: 320px;
      max-height: 280px;
      overflow: hidden;

      img {
        border-radius: 7px;
      }
    }
  }
}

@media (min-width:550px) {
   picture {
      max-width: 1024px;
    }
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
