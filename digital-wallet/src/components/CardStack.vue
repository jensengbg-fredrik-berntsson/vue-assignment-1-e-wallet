<template>
  <section class="cards">
    <div class="stacked" v-for="(card, index) in cards" :key="index" @click="changeCard(index)">
      <Card :input="card" />
    </div>
  </section>
</template>
<script>
import Card from "./Card";
export default {
  name: "CardStack",
  props: { cards: Array },
  components: { Card },
  methods: {
    changeCard(index) {
      this.$emit("changeCard", index);
    }
  }
};
</script>

<style scoped>
.cards {
  margin-top: 2rem;
}
.stacked {
  height: 4rem;
  overflow: visible;
  margin-top: -3rem;
  position: relative;
}
</style>
