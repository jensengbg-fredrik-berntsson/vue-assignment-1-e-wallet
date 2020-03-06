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
// @ is an alias to /src
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
      console.log(this.myCards[index]);
    },
    deleteCard() {
      console.log(this.input);
      this.myCards = JSON.parse(localStorage.getItem("cards"));
      let index = this.myCards.findIndex(x => x.nrInput == this.input.nrInput);
      console.log(index + " here");
      this.myCards.splice(index, 1);
      localStorage.setItem("cards", JSON.stringify(this.myCards));
    }
  },
  watch: {
    cards() {
      this.myCards = JSON.parse(localStorage.getItem("cards"));
    },
    activeCard() {
      this.activeCard = JSON.parse(localStorage.getItem("activeCard"));
    }
  }
};
</script>
<style >
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