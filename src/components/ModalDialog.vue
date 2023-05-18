<template>
  <div class="text-center">
    <v-dialog v-model="dialog" width="auto">
      <v-card>
        <v-card-text>
          <h2>Name: {{ packageInfo.name }}</h2>
          <h3>Version: {{ packageInfo.version }}</h3>
          <h4>Description: {{ packageInfo.description }}</h4>
          <h4>Keywords: {{ packageInfo.keywords }}</h4>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" block @click="dialog = false">
            Close Dialog
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    dialogProp: {
      type: Boolean,
      default: false,
    },
    packageProp: {
      type: Object,
      default: () => {},
    },
  },
  computed: {
    dialog: {
      get() {
        return this.dialogProp;
      },
      set(v) {
        this.$emit("updateDialog", v);
      },
    },
    packageInfo() {
      return this.packageProp.package;
    },
  },
};
</script>
