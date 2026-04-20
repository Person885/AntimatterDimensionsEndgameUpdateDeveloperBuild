<script>
export default {
  name: "StarContainer",
  props: {
    getStar: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      isUnlocked: false,
      amount: new Decimal(0),
      reward: new Decimal(0)
    };
  },
  computed: {
    star() {
      return this.getStar();
    },
    config() {
      return this.star.config;
    },
    description() {
      return this.config.description(this.reward);
    },
    rewardClassObject() {
      return {
        "o-star__container": true,
        [`o-star__container--${this.config.name}`]: true,
      };
    },
  },
  methods: {
    update() {
      this.isUnlocked = this.star.isUnlocked;
      this.amount.copyFrom(player.endgame.ethereal.stars[this.config.name]);
      this.reward.copyFrom(this.star.reward);
    },
    starReset() {
      resetForStar(this.star.id);
    }
  }
};
</script>

<template>
  <div
    v-if="star.isUnlocked"
    class="l-star-container"
  >
    <button
      :class="rewardClassObject"
    >
      <span>
        You have {{ format
      </span>
      <span>
        {{ description }}
      </span>
    </button>
  </div>
</template>

<style scoped>

</style>
