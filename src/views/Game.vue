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
          <p class="player-card-stats">
            {{playerCard.attack}}
          </p>
          <p class="player-card-stats">
            {{playerCard.defense}}
          </p>
        </div>
        <div>
          <img :src=playerCard.img alt="">
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
    background-color: lightslategray;
    border: 2px solid #42b983;
  }

  .player-card-info {
    flex-direction: row;
  }

  .player-card-stats {
    flex-direction: column;
    justify-content: space-between;
  }

  img {
    max-width: 75%;
    height: auto;
  }
</style>