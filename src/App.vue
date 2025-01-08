<script>
export default {
  data() {

  },
  methods: {

  }
}
</script>

<template>
  <img class="logo center" src="/src/assets/rpsls.webp" alt="rock paper scissors lizard spock image">

  <button id="start_game" class="center">Play game</button>
</template>

<style scoped>
.center {
  display: block;
  margin: auto;
}

.logo {
  width: 400px;
  /* margin-top: 0%; maybe change this from 20 - 0& after the game starts??? */
}

#start_game {
  margin-top: 1em;
}

button {
  padding: 1.2em;
  border-radius: 1em;
  border: none;
  background-color: #5fc5ba;
  text-transform: uppercase;
  font-weight: bold;
  font-size: 1em;
  letter-spacing: .2em;
  cursor: pointer;
  transition: 0.15s;
}

button:hover {
  /* background-color: #12a2d0; */
  background-color: #17133b;
  border: 2px solid #12a2d0;
  transition: 0.15s;
  color: white;
}
</style>
