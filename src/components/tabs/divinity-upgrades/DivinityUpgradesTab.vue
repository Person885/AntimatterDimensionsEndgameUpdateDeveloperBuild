<script>
import DivinityUpgradeButton from "./DivinityUpgradeButton";

export default {
  name: "DivinityUpgradesTab",
  components: {
    DivinityUpgradeButton
  },
  computed: {
    upgrades: () => DivinityUpgrade.all
  },
  methods: {
    id(row, column) {
      return (row - 1) * 5 + column - 1;
    }
  }
};
</script>

<template>
  <div class="l-divinity-upgrade-grid">
    <div
      v-for="row in 5"
      :key="row"
      class="l-divinity-upgrade-grid__row"
    >
      <DivinityUpgradeButton
        v-for="column in 5"
        :key="id(row, column)"
        :upgrade="upgrades[id(row, column)]"
      />
    </div>
  </div>
</template>

<style scoped>

</style>
