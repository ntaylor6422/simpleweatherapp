<template>
  <div class="searchContainer">
    <h1 v-if="!showSearch" v-on:click="handleClick">
      {{ selectedCity }}
    </h1>
    <div v-else class="seachItems">
      <input
        type="text"
        :placeholder="selectedCity"
        ref="cityInput"
        v-on:change="sendCity"
        v-on:blur="showSearch = false"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "Search",
  props: {
    selectedCity: String,
  },
  data: function() {
    return {
      showSearch: false,
    };
  },
  methods: {
    sendCity: function() {
      this.$emit("change-city", this.$refs.cityInput.value);
      this.showSearch = !this.showSearch;
    },
    handleClick: function() {
      this.showSearch = !this.showSearch;
    },
  },
  updated: function() {
    if (this.$refs.cityInput) {
      this.$refs.cityInput.focus();
    }
  },
};
</script>

<style scoped>
.searchContainer {
  grid-row: 1;
  grid-column: 1 / 5;
  display: flex;
  justify-content: center;
  align-items: center;
}

h1 {
  font-size: 45px;
  cursor: pointer;
}

h1:hover {
  color: rgb(51, 43, 154);
}

input {
  height: 10vh;
  width: 50vw;
  color: black;
  background: transparent;
  font-size: 45px;
  outline: none;
  border-radius: 10px;
  border: none;
}

::placeholder {
  color: rgba(0, 0, 0, 0.708);
}
</style>
