<template>
  <div id="app" class="small-container">
    <h1>Farms</h1>

    <farm-form @add:farm="addFarm" />
    <farm-table :farms="farms" />
  </div>
</template>

<script>
import FarmTable from "@/components/FarmTable.vue";
import FarmForm from "@/components/FarmForm.vue";

export default {
  name: "app",
  components: {
    FarmTable,
    FarmForm
  },
  data() {
    return {
      farms: [
        {
          id: 1,
          name: "Chuebodenalp",
          email: "chuebodenalp@schweiz.ch"
        },
        {
          id: 2,
          name: "Hinterfultigen",
          email: "hinterfultigen@gantrisch.ch"
        },
        {
          id: 3,
          name: "Uettligen",
          email: "uettligen@frienisberg.ch"
        }
      ]
    };
  },
  methods: {
    addFarm(farm) {
      const lastId =
        this.farms.length > 0 ? this.farms[this.farms.length - 1].id : 0;
      const id = lastId + 1;
      const newFarm = { ...farm, id };

      this.farms = [...this.farms, newFarm];
    }
  }
};
</script>

<style>
button {
  background: #009435;
  border: 1px solid #009435;
}

.small-container {
  max-width: 680px;
}
</style>