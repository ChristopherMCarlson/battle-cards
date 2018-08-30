<template>
  <div class="game">
    <div class="opponent">
      <div class="opponentCards" v-for="(opponetCard, index) in activeGame.players[1].hand" :key="index">
        {{opponetCard.name}}
      </div>
    </div>
    <div class="player">
      <div class="playerCards player-card" v-for="(playerCard, index) in activeGame.players[0].hand" :key="index">
        <div class="player-card-info">
          <div class="player-card-stats">
            <p>
              {{playerCard.attack}}
            </p>
          </div>
          <div class="player-card-stats">
            <p>
              {{playerCard.defense}}
            </p>
          </div>
        </div>
        <div>
          <img :src=playerCard.img alt="">
        </div>
        <div class="player-card-stats">
          <p>
            {{playerCard.health}}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
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
    }
  };
</script>

<style>
  .player {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin: 1% 3% 1% 3%;
    position: absolute;
    bottom: 50;
  }

  .opponent {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    margin: 1% 3% 1% 3%;
  }

  .player-card {
    flex-direction: column;
    justify-content: space-between;
    margin: 5% 3% 5% 3%;
    background-color: rgb(48, 53, 58);
    border: 2px solid #42b983;
  }

  .player-card-info {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 0% 10% 0% 10%;
  }

  .player-card-stats {
    display: flex;
    flex-direction: column;
  }

  img {
    max-width: 75%;
    height: auto;
  }

  .game {
    height: 100vh;
  }
</style>