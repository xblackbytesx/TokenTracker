<template>
  <div class="coin-ticker" @dblclick.stop="openDetails">
    <div class="coin-ticker__info">
      <div>{{ info.name }}</div>
      <div>
        <div class="coin-ticker__icon">
          <span :style="{ backgroundImage: 'url(' + iconbase + ')' }"></span>
        </div>
        <div class="coin-ticker__pair">
          <b>{{ info.base }}</b
          >/{{ info.quote }}
        </div>
        <div class="coin-ticker__price" v-if="ticker.price">
          {{ ticker.price || "" }} <span>{{ info.quote }}</span>
        </div>
      </div>
      <div
        :class="[ticker.percent < 0 ? 'down' : 'up', 'col-5', 'text-right']"
        v-if="ticker.price"
      >
        <div class="coin-per">
          <span class="indicator"></span><span>{{ ticker.percent }}%</span>
        </div>
        <div class="coin-chg">
          {{ parseFloat(ticker.chg).toFixed(info.quote === "USDT" ? 3 : 8) }}
        </div>
        <div>
          <span class="text-secondary">Vol:</span>
          <span class="text-dark">{{ ticker.vol }}</span>
        </div>
      </div>
      <div
        class="dd-container"
        :class="[{ show: showDropDown }]"
        v-click-outside="closeDropDown"
      >
        <span role="button" class="menu-btn" @click.stop="onDropDown">
          <i class="fa fa-ellipsis-v" aria-hidden="true"></i>
        </span>
        <div class="dd-menu" v-if="showDropDown">
          <span class="dd-item" @click="openDetails">Open</span>
          <span class="dd-item" @click="removeCard">Delete</span>
        </div>
      </div>
    </div>
    <div class="coin-ticker__chart" v-if="ticker.price">
      <Sparkline :cdata="ticker.price" :width="380" :height="90"></Sparkline>
    </div>
  </div>
</template>
<script>
import Sparkline from "./Sparkline.vue";
import { unSubscribeSymbol } from "../services/binance";
export default {
  props: ["ticker", "info"],
  data() {
    return {
      showDropDown: false,
      iconbase:
        "https://raw.githubusercontent.com/rainner/binance-watch/master/public/images/icons/" +
        this.info.base.toLowerCase() +
        "_.png"
    };
  },
  methods: {
    onDropDown() {
      this.showDropDown = true;
    },
    removeCard() {
      this.showDropDown = false;
      unSubscribeSymbol(this.info.symbol);
      this.$store.commit("REMOVE_COIN_PAIR", this.info.symbol);
    },
    openDetails() {
      this.showDropDown = false;
      this.$router.push({
        name: "infoview",
        params: { symbol: this.info.symbol }
      });
    },
    closeDropDown() {
      this.showDropDown = false;
    }
  },
  components: {
    Sparkline
  }
};
</script>
<style>
.coin-ticker {
  position: relative;
  min-height: 250px;
  overflow: hidden;

  &__info {
    padding: 16px;
  }

  &__chart {
    position: absolute;
    bottom: -4px;
    width: 103%;
  }
}
</style>
