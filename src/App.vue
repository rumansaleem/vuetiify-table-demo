<template>
  <v-app class="App">
    <v-main>
      <stocks-table-page></stocks-table-page>
    </v-main>
  </v-app>
</template>

<script>
import StocksTablePage from "./components/StocksTablePage";

export default {
  name: "App",
  components: {
    StocksTablePage,
  },
};
</script>

