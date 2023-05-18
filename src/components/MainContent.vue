<template>
  <div>
    <div class="d-flex align-center mb-2 w-50 ma-auto">
      <v-text-field v-model="searchValue" label="Search" hide-details />
      <v-btn class="ml-3" @click="getPackageData">Find</v-btn>
    </div>
    <div class="w-75 ma-auto">
      <PaginationTable :packages="packages" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import PaginationTable from "@/components/PaginationTable";

export default {
  name: "HelloWorld",
  components: {
    PaginationTable,
  },
  data() {
    return {
      searchValue: "",
      packages: [],
    };
  },
  methods: {
    async getPackageData() {
      if (!this.searchValue) return;

      try {
        const { data } = await axios.get(
          `https://registry.npmjs.org/-/v1/search?text=${this.searchValue}&size=100`
        );
        this.packages = [...data.objects];
      } catch (e) {
        console.error(e);
      }
    },
  },
};
</script>

<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
