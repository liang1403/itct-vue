<template>
  <div class="boxer-card">
    <img class="boxer-photo" :src="boxer.photo" />

    <!-- :class="[isPro ? 'pro-boxer' : 'amateur-boxer']" -->
    <div
      :class="[
        'boxer-name',
        {
          'pro-boxer': isPro,
          'amateur-boxer': !isPro,
        },
      ]"
    >
      {{ boxer.name }}
      <img
        class="boxer-pro-icon"
        v-if="isPro"
        :src="require('@/assets/champion-belt.png')"
      />
    </div>

    <hr class="solid" />

    <div class="boxer-titles">
      <div
        class="boxer-title-item"
        v-for="(title, index) in boxer.titles"
        :key="index"
      >
        {{ title }}
      </div>
    </div>
    <div v-if="!isPro" class="boxer-request-btn">
      <button @click="upgrade">Upgrade</button>
      <loader v-if="isLoading" />
    </div>
  </div>
</template>

<script>
import WeightCategory from "@/constants/WeightCategory";
import BoxerStatus from "@/constants/BoxerStatus";
import Loader from "@/components/DotsLoader.vue";

export default {
  /**
   *
   *
   *
   **/
  components: {
    Loader,
  },

  /**
   *
   *
   *
   **/
  props: {
    boxer: {
      type: Object,
      required: true,
    },

    // item: Object
  },

  /**
   *
   *
   *
   **/
  data: () => ({
    isLoading: false,
  }),

  /**
   *
   *
   *
   **/
  computed: {
    categoryByWeight() {
      return Object.keys(WeightCategory).find((key) => {
        const category = WeightCategory[key];
        return (
          (!category.min || this.boxer.weight >= category.min) &&
          (!category.max || this.boxer.weight < category.max)
        );
      });
    },
    isPro() {
      return this.boxer.status === BoxerStatus.Pro;
    },
  },

  /**
   *
   *
   *
   **/
  methods: {
    async upgrade() {
      this.isLoading = true;

      await this.stall();
      this.$emit('upgrade');
      
      this.isLoading = false;
    },
    stall() {
      return new Promise((resolve) => setTimeout(resolve, 500));
    },
  },

  /**
   *
   *
   *
   **/
  created() {},

  /**
   *
   *
   *
   **/
  mounted() {},

  /**
   *
   *
   *
   **/
  watch: {},
};
</script>

<style lang="scss">
.boxer-card {
  background: #2d2d2d;
  width: 400px;
  padding: 10px;
  box-shadow: 0 3px 1px -2px rgba(0, 0, 0, 0.2), 0 2px 2px 0 rgba(0, 0, 0, 0.14),
    0 1px 5px 0 rgba(0, 0, 0, 0.12);
  text-align: left;

  .boxer-photo {
    width: 100%;
  }

  .boxer-name {
    display: flex;
    align-items: center;
    font-weight: bold;
    font-size: 1.5rem;

    &.pro-boxer {
      color: gold;
    }
    &.amateur-boxer {
      color: silver;
    }
    .boxer-pro-icon {
      width: 28px;
      margin-left: 8px;
      padding-bottom: 4px;
    }
  }

  hr.solid {
    border-top: 3px solid silver;
  }

  .boxer-titles {
    margin-top: 10px;
    .boxer-title-item {
      color: silver;
    }
  }

  .boxer-request-btn {
    display: flex;
    margin-top: 16px;
    button {
      background-color: gold;
      color: #262626;
      font-weight: bold;
      border: none;
      padding: 15px;
      min-height: 30px;
      min-width: 120px;
      cursor: pointer;
    }
  }
}
</style>
