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
      gameInfo: '',
      gameState: 'start',
      gameStateOptions: {
        START: 'start',
        PLAYING: 'playing',
        GAME_OVER: 'game over'
      }
    }
  },
  methods: {
    setGameState: function (state) {
      this.gameState = state;
    },
    startGame: function () {
      this.setGameState(this.gameStateOptions.PLAYING);
      this.resetGame();
    },
    endGame: function () {
      this.setGameState(this.gameStateOptions.GAME_OVER);
    },
    resetGame: function () {
      this.playerScore = 0;
      this.computerScore = 0;
      this.playerChoice = '',
        this.computerChoice = ''
    },
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

  <div id="logic-buttons-container">
    <button v-if="gameState == gameStateOptions.START" aria-label="play game" @click="startGame" class="center">Play
      game</button>
    <button v-else-if="gameState == gameStateOptions.PLAYING" aria-label="end game" @click="endGame" class="center">End
      game</button>
    <button v-else="gameState == gameStateOptions.GAME_OVER" aria-label="play again" @click="startGame"
      class="center">Play
      Again?</button>
  </div>


  <div v-if="gameState == gameStateOptions.PLAYING" id="game-buttons-container">
    <button v-for="choice in choiceOptions" aria-label="{{choice}} button" @click="setPlayerChoice(choice)">{{ choice
      }}</button>
  </div>

  <div class="score-container">
    <div id="player-score">
      <p class="score-text">Your Score</p>
      <h1 class="score">{{ playerScore }}</h1>
    </div>

    <div id="computer-score">
      <p class="score-text">Computer Score</p>
      <h1 class="score">{{ computerScore }}</h1>
    </div>
  </div>
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

#logic-buttons-container {
  margin-top: 1em;
}

#game-buttons-container {
  display: flex;
  flex-direction: row;
  margin-top: 1em;
  justify-content: space-around;
  flex-wrap: wrap;
}

#game-buttons-container>button {
  margin-top: 1em;
}

.score-text {
  color: white;
  font-size: 2em;
}

.score {
  color: white;
  font-size: 4em;
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
  transition: all ease-in-out .2s;
}

button:hover {
  background-color: #17133b;
  border: 2px solid #12a2d0;
  color: white;
  transform: translateY(-5px);
}

button:disabled {
  opacity: .2;
  cursor: not-allowed;
}

.score-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  text-align: center;
}

#player-score,
#computer-score {
  border: 2px solid white;
  border-radius: 2em;
  margin: 2em;
  margin-top: 4em;
  padding: 1em;
  padding-bottom: 0;
  width: 10em;
}

.score-container .score-text {
  margin-bottom: 0px;
}

.score-container .score {
  margin-top: 0px;
}
</style>
