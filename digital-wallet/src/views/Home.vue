<template>
  <div class="home">
    <Top header="E-WALLET" current="ACTIVE CARD" />
    <Card :input="input" />
    <CardStack :cards="myCards" @changeCard="changeCard" />
    <button class="Btn remove" @click="deleteCard">DELETE CARD</button>
    <button class="Btn" @click="addCard">ADD A NEW CARD</button>
  </div>
</template>

<script>
import Top from "../components/Top";
import Card from "../components/Card";
import CardStack from "../components/CardStack";
export default {
  name: "Home",
  components: {
    Top,
    Card,
    CardStack
  },
  data: () => {
    return {
      input: {},
      cards: localStorage.getItem("cards"),
      myCards: []
    };
  },
  mounted() {
    if (localStorage.getItem("cards")) {
      this.myCards = JSON.parse(localStorage.getItem("cards"));
    } else {
      localStorage.setItem("cards", JSON.stringify(this.myCards));
    }
    if (localStorage.getItem("activeCard")) {
      this.input = JSON.parse(localStorage.getItem("activeCard"));
    }
  },

  methods: {
    addCard() {
      this.$router.push("/AddCard");
    },
    changeCard(index) {
      this.input = this.myCards[index];
      localStorage.setItem("activeCard", JSON.stringify(this.input));
    },
    deleteCard() {
      let index = this.myCards.findIndex(x => x.nrInput == this.input.nrInput);
      this.myCards.splice(index, 1);

      localStorage.setItem("cards", JSON.stringify(this.myCards));

      this.input = {};
      localStorage.setItem("activeCard", JSON.stringify(this.input));
    }
  },
  watch: {
    cards() {
      this.myCards = JSON.parse(localStorage.getItem("cards"));
    }
  }
};
</script>
<style>
/* använder samma styleing på alla 3 knappar, 2 här och 1 på AddCard */
.Btn {
  width: 24rem;
  height: 5rem;
  border: 1px solid #000000;
  background: white;
  border-radius: 0.5rem;
  font-size: 1.4rem;
  font-weight: 900;
  position: absolute;
  bottom: 3rem;
}
.remove {
  bottom: 8.5rem;
}
</style>
