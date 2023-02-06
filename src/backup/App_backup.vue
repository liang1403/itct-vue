<template>
  <div class="boxer-card-wrapper">
    <!-- <boxer-card :boxer="boxer" @upgrade="upgradeBoxer(boxer)" /> -->
    <boxer-card
      v-for="(boxer, index) in boxers"
      :boxer="boxer"
      :key="index"
      @upgrade="upgradeBoxer(boxer)"
    />
  </div>
</template>

<script>
import BoxerCard from "@/components/BoxerCard.vue";
import BoxerStatus from "@/constants/BoxerStatus";

export default {
  name: "App",
  components: {
    BoxerCard,
  },
  data: () => ({
    boxer: {
      name: "IGOR NESTEROV",
      photo:
        "https://rtfight.com/back/api/contactfile/photo/0dddda14-1a2c-4c42-8342-7163458a461c",
      status: BoxerStatus.Amateur,
      weight: 79,
      titles: ["Best Amateur Boxer 2021", "Best Amateur Boxer 2022"],
    },
    boxers: [
      {
        name: "BEATRISE ROZENTALE",
        photo:
          "https://rtfight.com/back/api/contactfile/photo/eed75720-9deb-4e7b-ab0c-6f22a3eb0693",
        status: BoxerStatus.Amateur,
        weight: 67,
        titles: [],
      },
      {
        name: "DANIEL LAPIN",
        photo:
          "https://rtfight.com/back/api/contactfile/photo/4a0311b7-b4b4-44d1-8e83-22cdc908234f",
        status: BoxerStatus.Pro,
        weight: 96,
        titles: ["Best Pro Boxer 2022", "Best Pro Boxer 2023"],
      },
      {
        name: "ISLAM ISMAILOV",
        photo:
          "https://rtfight.com/back/api/contactfile/photo/56844a0b-68bb-4ead-8022-34466c55ca2d",
        status: BoxerStatus.Amateur,
        weight: 82,
        titles: [],
      },
    ],
  }),
  methods: {
    upgradeBoxer(boxer) {
      boxer.status = BoxerStatus.Pro;
    },
  },
};
</script>

<style>
body {
  background: #262626;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}

.boxer-card-wrapper {
  display: flex;
  justify-content: center;
  align-items: baseline;
  gap: 15px;
}
</style>
