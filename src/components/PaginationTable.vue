<template>
  <div>
    <v-table style="min-height: 576px">
      <thead>
        <tr>
          <th class="text-left">Name</th>
          <th class="text-left">Versions</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(item, index) in currentPage"
          :key="index"
          @click="updateDialog(true, item)"
          class="table-item"
        >
          <td class="text-left">{{ item.package.name }}</td>
          <td class="text-left">{{ item.package.version }}</td>
        </tr>
      </tbody>
    </v-table>
    <v-pagination
      v-model="page"
      :length="maxPagesLen"
      rounded="circle"
    ></v-pagination>
    <ModalDialog
      :package-prop="dialogPackage"
      :dialog-prop="isShowDialog"
      @updateDialog="updateDialogVisible"
    />
  </div>
</template>

<script>
import _ from "lodash";
import ModalDialog from "@/components/ModalDialog";

export default {
  data() {
    return {
      maxPagesLen: 10,
      page: 1,
      isShowDialog: false,
      dialogPackage: {},
    };
  },
  components: {
    ModalDialog,
  },
  props: {
    packages: {
      type: Array,
      default: () => [],
    },
  },
  watch: {
    packages() {
      this.maxPagesLen = this.packages.length / 10;
    },
  },
  computed: {
    currentPage() {
      const dividedArray = _.chunk(this.packages, 10);
      return dividedArray[this.page - 1];
    },
  },
  methods: {
    updateDialog(visible, props) {
      this.updateDialogVisible(visible);
      this.updateDialogProp(props);
    },
    updateDialogVisible(v) {
      this.isShowDialog = v;
    },
    updateDialogProp(v) {
      this.dialogPackage = { ...v };
    },
  },
};
</script>

<style scoped lang="scss">
.table-item {
  :hover {
    cursor: pointer;
    opacity: 0.7;
  }
}
</style>
