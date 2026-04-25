<script>
import DivinityMilestoneButton from "./DivinityMilestoneButton";

export default {
  name: "DivinityMilestonesTab",
  components: {
    DivinityMilestoneButton
  },
  data() {
    return {
      divinityCount: 0,
    };
  },
  computed: {
    milestones() {
      return Object.values(GameDatabase.celestials.divinityMilestones)
        .sort((a, b) => a.divinities - b.divinities)
        .map(config => new DivinityMilestoneState(config));
    },
    rows() {
      return Math.ceil(this.milestones.length / 3);
    }
  },
  methods: {
    update() {
      this.divinityCount = Math.floor(Currency.divinities.value);
    },
    getMilestone(row, column) {
      return () => this.milestones[(row - 1) + column - 1];
    }
  }
};
</script>

<template>
  <div class="l-divinity-milestone-grid">
    <div>You have {{ quantify("Divinity", divinityCount, 3) }}.</div>
    <div
      v-for="row in rows"
      :key="row"
      class="l-divinity-milestone-grid__row"
    >
      <DivinityMilestoneButton
        v-for="column in 1"
        :key="row + column"
        :get-milestone="getMilestone(row, column)"
        class="l-divinity-milestone-grid__cell"
      />
    </div>
  </div>
</template>

<style scoped>

</style>
