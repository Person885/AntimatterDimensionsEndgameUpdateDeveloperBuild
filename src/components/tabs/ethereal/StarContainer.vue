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
    };
  },
  computed: {
    star() {
      return this.getStar();
    },
    reward() {
      return this.star.reward;
    },
    description() {
      return this.star.config.description(this.reward);
    },
    rewardClassObject() {
      return {
        "o-star__container": true,
        [`o-star__container--${star.config.name}`]: true,
      };
    },
  },
  methods: {
    update() {
      this.isUnlocked = this.star.isUnlocked;
    },
    starReset() {
      resetForStar(this.star.id);
    }
  }
};
</script>

<template>
  <div
    v-if="config.isUnlocked"
    class="l-star-container"
  >
    <button
      :class="rewardClassObject"
    >
      <span>
        {{ reward }}
      </span>
    </button>
  </div>
</template>

<style scoped>

</style>
