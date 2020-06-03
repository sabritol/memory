<template>
  <div id="app">
    <h2>Memory card game</h2>

    <transition name="fade"> </transition>

    <form @submit.prevent="startGame">
      <span>Choose the number of cards.</span>
      <br />
      <br />
      <input type="radio" id="4" value="4" v-model="picked" />
      <label for="4">4</label>
      <br />
      <input type="radio" id="8" value="8" v-model="picked" />
      <label for="8">8</label>

      <input type="radio" id="12" value="12" v-model="picked" />
      <label for="12">12</label>
      <br />
      <br />
      <cards-table v-show="display"> </cards-table>
      <button @click="display = !display">Start new game</button>
    </form>
    <transition name="fade">
      <modal
        v-if="$store.state.modal"
        @closed="
          $store.commit('hideModal');
          $store.commit('resetValues');
        "
        :title="$store.state.modal.title"
        :message="$store.state.modal.message"
      />
    </transition>
  </div>
</template>

<style lang="scss">
:root {
  --main-color: rgb(255, 255, 255);
  --bg-color: rgb(0, 5, 82);
}
body {
  background: rgb(255, 255, 255);
  color: var(--main-color);
  text-shadow: 0 0 6px black;
}
#app {
  input,
  button {
    padding: 10px;
    border-radius: 5px;
  }
  input {
    margin: 0 10px;
    text-shadow: 0 0 6px black;
  }
  span {
    font-size: 16px;
    vertical-align: middle;
  }
  button {
    background-color: var(--main-color);
    color: rgb(0, 5, 82);
    border: none;
    cursor: pointer;
    transition: box-shadow 0.2s ease-in;
    text-shadow: 0 0 6px rgb(71, 72, 77);
  }
  button:hover {
    box-shadow: 2px 2px 0 grey;
  }
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  background-color: var(--bg-color);
  padding: 20px 10px;
  max-width: 600px;
  margin: 80px auto;
  border-radius: 5px;
  border: 1px solid grey;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.9s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
