<template>
  <v-container style="height: 100vh">
    <v-combobox
      :items="columnNames"
      v-model="selectedColumnNames"
      dense
      multiple
      outlined
      small-chips
      label="Columns"
    ></v-combobox>
    <v-data-table
      dense
      :headers="selectedColumns"
      :items="stocks"
      :items-per-page="5"
      class="elevation-1"
    >
      <template
        v-for="numericField in numericFields"
        v-slot:[numericField]="{ value }"
      >
        {{ formatNumber(value) }}
      </template>
    </v-data-table>
    <v-btn class="m-2" fab dark small color="primary">
      <v-icon dark> mdi-refresh </v-icon>
    </v-btn>
  </v-container>
</template>

<script>
import stocksData from "./stocks";
// import axios from "axios";

export default {
  methods: {
    formatNumber(num) {
      return Number(num).toFixed(2);
    },
    loadStocksData() {
      // axios.get("https://api.url", {
      //   headers: {"Authorization": "Bearer: token"}
      // }).then(res => res.data)
      // .then(data => this.stocks = data);

      this.stocks = stocksData;
    },
  },
  computed: {
    columnNames() {
      return this.columns.map((c) => c.text).filter((c) => c !== "Name");
    },
    selectedColumns() {
      return this.columns.filter((c) =>
        ["Name", ...this.selectedColumnNames].includes(c.text)
      );
    },
  },
  data() {
    return {
      numericFields: [
        "item.keyLevelMetric.latestPrice",
        "item.percentChangeMetric.openPrice",
        "item.percentChangeMetric.closePrice",
        "item.bullStrengthMetric.bullStrength",
        "item.bullStrengthMetric.bearStrength",
        "item.bullStrengthMetric.bullStrengthRatio",
      ],
      selectedColumnNames: ["Open Price", "Close Price", "Latest Price"],
      columns: [
        { text: "Name", value: "scrip", sortable: false },
        {
          text: "Bull Strngth",
          align: "end",
          value: "bullStrengthMetric.bullStrength",
        },
        {
          text: "Bear Strngth",
          align: "end",
          value: "bullStrengthMetric.bearStrength",
        },
        {
          text: "Bull Stgth Ratio",
          align: "end",
          value: "bullStrengthMetric.bullStrengthRatio",
        },
        {
          text: "Latest Price",
          align: "end",
          value: "keyLevelMetric.latestPrice",
        },
        {
          text: "Open Price",
          align: "end",
          value: "percentChangeMetric.openPrice",
        },
        {
          text: "Close Price",
          align: "end",
          value: "percentChangeMetric.closePrice",
        },
        {
          text: "Percent Change",
          align: "end",
          value: "percentChangeMetric.percentChange",
        },
      ],
      stocks: stocksData,
    };
  },
};
</script>