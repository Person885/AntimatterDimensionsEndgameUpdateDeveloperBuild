<script>
import DivineDimensionRow from "./ClassicDivineDimensionRow";
import PrimaryButton from "@/components/PrimaryButton";

export default {
  name: "ClassicDivineDimensionTab",
  components: {
    PrimaryButton,
    DivineDimensionRow
  },
  data() {
    return {
      divineMatter: new Decimal(0),
      matterPerSecond: new Decimal(0),
      incomeType: "",
      conversionFormula1: new Decimal(0),
      conversionFormula2: 0,
      conversionFormula3: 0,
      creditsClosed: false,
    };
  },
  methods: {
    update() {
      this.divineMatter.copyFrom(Currency.divineMatter);
      this.matterPerSecond.copyFrom(DivineDimension(1).productionPerRealSecond);
      this.incomeType = "Divine Matter";
      this.conversionFormula1 = DivineDimensions.conversionFormula1;
      this.conversionFormula2 = DivineDimensions.conversionFormula2;
      this.conversionFormula3 = DivineDimensions.conversionFormula3;
      this.creditsClosed = GameEnd.creditsEverClosed;
    },
    maxAll() {
      DivineDimensions.buyMax();
    },
  }
};
</script>

<template>
  <div class="l-divine-dim-tab">
    <div class="c-subtab-option-container">
      <PrimaryButton
        class="o-primary-btn--subtab-option"
        @click="maxAll"
      >
        Max all
      </PrimaryButton>
    </div>
    <div>
      <p>
        You have
        <span class="c-celestial-dim-description__accent">{{ format(divineMatter, 2, 1) }}</span>
        Divine Matter,
        <br>
        translated to a
        <span class="c-divine-dim-description__accent">
          {{ formatX(conversionFormula1, 2, 2) }}
        </span>
        multiplier to Endgame and Ethereal Power gain, a
        <span class="c-divine-dim-description__accent">
          {{ formatPow(conversionFormula2, 2, 3) }}
        </span>
        to Antimatter Exponent while Doomed, and a
        <span class="c-divine-dim-description__accent">
          {{ formatPercents(conversionFormula3, 2, 2) }}
        </span>
        reduction to Hadron and Remnants of Alpha Decay cap times.
      </p>
    </div>
    <div>You are getting {{ format(matterPerSecond, 2, 0) }} {{ incomeType }} per second.</div>
    <div class="l-dimensions-container">
      <DivineDimensionRow
        v-for="tier in 8"
        :key="tier"
        :tier="tier"
      />
    </div>
  </div>
</template>
