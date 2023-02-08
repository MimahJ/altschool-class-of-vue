<template>
  <div>{{ selectedColor }}</div>

  <input v-model="searchValue" />

  <div v-for="color in filteredColors" :key="color">
    <Color :value="color" @change-selected-color="selectedColor = $event">
      <template #color="slotProps">{{ slotProps.value }}</template>

      <template #footer>
        <div style="font-size: 8px">color details</div>
      </template>
    </Color>
  </div>
</template>

<script setup>
import { ref, computed, watch } from "vue";

import Color from "./Color.vue";

const name = "Hello World";
const selectedColor = ref("No color selected..");
const colors = ["red", "blue", "green", "yellow", "pink", "black", "gold"];

const filteredColors = computed(() => {
  return colors.filter((item) =>
    item.toLowerCase().includes(searchValue.value.toLowerCase())
  );
});

const searchValue = ref("");

const filterString = () => {
  // loop through the colors
  // get color
  // do check to confirm if searchvalue is in the currentColor

  const newArray = [];

  if (searchValue.value.length === 0) {
    return colors;
  }

  for (let index = 0; index < colors.length; index++) {
    const color = colors[index];

    // check if the color is included in the searchValue
    let condition = color
      .toLowerCase()
      .includes(searchValue.value.toLowerCase());

    if (condition) {
      newArray.push(color);
    }
  }

  return newArray;
};

watch(searchValue, () => {
  filteredColors.value = colors.filter((item) =>
    item.toLowerCase().includes(searchValue.value.toLowerCase())
  );
});

const getGreeting = () => {
  return "Hello guys";
};

/* export default {
  name: "Recap_01_02_2023",
  components: { Color },
  data() {
    return {
      name: "Hello World",
      selectedColor: "No color selected..",
      colors: ["red", "blue", "green", "yellow", "pink", "black", "gold"],
      filteredColors: [
        "red",
        "blue",
        "green",
        "yellow",
        "pink",
        "black",
        "gold",
      ],
      searchValue: "",
    };
  },
  methods: {
    filterString() {
      // loop through the colors
      // get color
      // do check to confirm if searchvalue is in the currentColor

      const newArray = [];

      if (this.searchValue.length === 0) {
        return this.colors;
      }

      for (let index = 0; index < this.colors.length; index++) {
        const color = this.colors[index];

        // check if the color is included in the searchValue
        let condition = color
          .toLowerCase()
          .includes(this.searchValue.toLowerCase());

        if (condition) {
          newArray.push(color);
        }
      }

      return newArray;
    },
  },
  watch: {
    searchValue: {
      handler() {
        this.filteredColors = this.colors.filter((item) =>
          item.toLowerCase().includes(this.searchValue.toLowerCase())
        );
      },
    },
  },
  computed: {
    filteredColorsComputed() {
      return this.colors.filter((item) =>
        item.toLowerCase().includes(this.searchValue.toLowerCase())
      );
    },
    getGreeting() {
      return "Hello guys";
    },
  },
}; */
</script>