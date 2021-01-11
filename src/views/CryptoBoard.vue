<template>
  <div class="cards">
    <div class="card" v-for="(value, index) in currencies" :key="index">
      <CurrencyCard
        :ticker="tickers[value.symbol] || {}"
        :info="value"
      ></CurrencyCard>
    </div>
  </div>
</template>
<script>
import CurrencyCard from "../components/CurrencyCard.vue";
import { mapState } from "vuex";
export default {
  name: "CryptoBoard",
  components: {
    CurrencyCard
  },
  computed: {
    ...mapState(["tickers", "currencies"])
  }
};
</script>
<style>
.cards {
  display: flex;
  flex-flow: row wrap;

  .card {
    flex: 1 1 400px;
  }
}
</style>
