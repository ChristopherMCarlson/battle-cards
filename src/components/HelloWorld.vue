<template>
  <div>
    <h1>Please input name</h1>
    <form @submit.prevent="startGame($event)">
      <input type="text" name="name" autocomplete="off" placeholder="Competitor"><br>
      <button class="new-game-button" type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    props: {
      msg: String
    },
    methods: {
      startGame(event) {
        this.$store.dispatch("startGame", event.target.name.value)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  h3 {
    margin: 40px 0 0;
  }

  a {
    color: #42b983;
  }

  input[type=text] {
    background: transparent;
    border: none;
    border-bottom: 1px solid #9e9e9e;
    text-align: center;
    color: #ffffff;
    width: 25%;
    font-size: 1rem;
  }

  input:focus {
    outline: #26374d;
  }

  .new-game-button {
    margin-top: 1rem;
    background-color: #070a0e;
    border-radius: 12px;
    border: 2px solid #42b983;
    color: #ffffff;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
  }
</style>