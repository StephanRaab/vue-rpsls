<script>
export default {
  data() {
    return {
      playerScore: 0,
      computerScore: 0,
      choiceOptions: ['rock', 'paper', 'scissors', 'lizard', 'spock'],
      playerChoice: '',
      computerChoice: '',
      winningConditions: {
        rock: ['scissors', 'lizard'],
        paper: ['rock', 'spock'],
        scissors: ['paper', 'lizard'],
        lizard: ['paper', 'spock'],
        spock: ['rock', 'scissors']
      },
      gameInfo: ''
    }
  },
  methods: {
    setPlayerChoice: function (selection) {
      this.playerChoice = selection;
      this.generateComputerChoice();
      this.checkWinner();
    },
    generateComputerChoice: function () {
      let computerIndex = Math.floor(Math.random() * this.choiceOptions.length);
      this.computerChoice = this.choiceOptions[computerIndex];
    },
    checkWinner: function () {
      if (this.playerChoice === this.computerChoice) {
        this.gameInfo = "It's a tie!"
      } else if (this.winningConditions[this.playerChoice].includes(this.computerChoice)) {
        this.playerScore++;
      } else {
        this.computerScore++;
      }
    }
  }
}
</script>

<template>
  <img class="logo center" src="/src/assets/rpsls.webp" alt="rock paper scissors lizard spock image">

  <button id="start-game" class="center">Play game</button>


  <div id="game-btns-container">
    <button v-for="choice in choiceOptions" @click="setPlayerChoice(choice)">{{ choice }}</button>
  </div>

  <p class="score">Your Score: {{ playerScore }}</p>
  <p class="score">Computer Score: {{ computerScore }}</p>
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

#start-game {
  margin-top: 1em;
}

#game-btns-container {
  display: flex;
  flex-direction: row;
  margin-top: 1em;
  justify-content: space-around;
}

.score {
  color: white;
  font-size: 2em;
}

button {
  padding: 1.2em;
  border-radius: 1em;
  border: 2px solid transparent;
  background-color: #5fc5ba;
  text-transform: uppercase;
  font-weight: bold;
  font-size: 1em;
  letter-spacing: .2em;
  cursor: pointer;
  transition: 0.2s;
}

button:hover {
  /* background-color: #12a2d0; */
  background-color: #17133b;
  border: 2px solid #12a2d0;
  transition: 0.2s;
  color: white;
}
</style>
