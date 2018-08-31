<template>
  <div class="game">
    <div v-if="activeGame.over == false">
      <div class="opponent">
        <div class="opponentCards card" v-for="(opponentCard, index) in activeGame.players[1].hand" :key="index" @click='opponentCardId = opponentCard.id'>
          <div v-bind:class="{'card-hide': !opponentCard.visible}">
            <div class="card-info">
              <div class="card-stats">
                <p>
                  {{opponentCard.attack}}
                </p>
              </div>
              <div class="card-stats">
                <p>
                  {{opponentCard.defense}}
                </p>
              </div>
            </div>
            <div>
              <img :src=opponentCard.img alt="">
            </div>
            <div class="card-stats">
              <p>
                {{opponentCard.health}}
              </p>
            </div>
          </div>
        </div>
      </div>
      <div>
        <button @click="fight()" class="fight-button">Fight!</button>
      </div>
      <div class="player">
        <div class="playerCards card" v-for="(playerCard, index) in activeGame.players[0].hand" :key="index" @click='playerCardId = playerCard.id'>
          <div class="card-info">
            <div class="card-stats">
              <p>
                {{playerCard.attack}}
              </p>
            </div>
            <div class="card-stats">
              <p>
                {{playerCard.defense}}
              </p>
            </div>
          </div>
          <div>
            <img :src=playerCard.img alt="">
          </div>
          <div class="card-stats">
            <p>
              {{playerCard.health}}
            </p>
          </div>
        </div>
      </div>
    </div>
    <div v-else>
      <div v-if="activeGame.winner.name == activeGame.players[0].name">
        <p>You win!</p>
      </div>
      <div v-else-if="activeGame.winner.name == activeGame.players[1].name">
        <p>You lose!</p>
      </div>
      <div v-else>
        <p>Tie game</p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Game',
    data() {
      return {
        "playerId": this.$store.state.game.players[0].id,
        "playerCardId": "",
        "opponentId": this.$store.state.game.players[1].id,
        "opponentCardId": ""
      }
    },
    mounted() {
      let id = this.$route.params.id;
      if (!this.activeGame.id) {
        this.$store.dispatch("getGame", id);
      }
    },
    computed: {
      activeGame() {
        return this.$store.state.game;
      }
    },
    methods: {
      fight() {
        let fightObj = {
          "playerId": this.$store.state.game.players[0].id,
          "playerCardId": this.playerCardId,
          "opponentId": this.$store.state.game.players[1].id,
          "opponentCardId": this.opponentCardId,
        }
        console.log(fightObj)
        this.$store.dispatch("fight", fightObj)
      }
    }
  };
</script>

<style>
  .player {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin: 0% 3% 0% 3%;
  }

  .opponent {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    margin: 0% 3% 0% 3%;
  }

  .opponent-card {
    flex-direction: column;
    justify-content: space-between;
    margin: 1% 3% 1% 3%;
    background-color: rgb(48, 53, 58);
    border: 2px solid #42b983;
    cursor: pointer;
  }

  .card {
    flex-direction: column;
    justify-content: space-between;
    margin: 1% 3% 1% 3%;
    background-color: rgb(48, 53, 58);
    border: 2px solid #42b983;
    cursor: pointer;
  }

  .card-info {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 0% 10% 0% 10%;
  }

  .player-card-info {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 0% 10% 0% 10%;
  }

  .card-stats {
    display: flex;
    flex-direction: column;
  }

  img {
    max-width: 75%;
    height: auto;
  }

  .card-hide {
    visibility: hidden;
  }

  .card-show {
    visibility: visible;
  }

  .game {
    align-items: center;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 95vh;
  }

  .fight-button {
    background-color: #070a0e;
    border-radius: 12px;
    border: 2px solid #42b983;
    color: #ffffff;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    transition: background-color 300ms;
    cursor: pointer;
  }

  .fight-button:hover {
    background-color: #42b983;

  }

  .button-hide {
    visibility: hidden;
  }
</style>