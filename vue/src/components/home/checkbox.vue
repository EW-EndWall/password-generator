<script>
export default {
  name: "Checkbox",
  props: {
    titleData: String,
    valueData: Boolean,
    changeConfig: Function,
    detail: String,
  },
  data() {
    return {
      valData: this.valueData,
    };
  },
  methods: {
    changeCheckbox() {
      this.$emit("change-checkbox", [this.titleData, this.valData]);
      // * generate password
      this.changeConfig();
    },
  },
};
</script>

<template>
  <div>
    <div v-if="!this.detail" class="flex items-center mb-4">
      <input
        @change="changeCheckbox"
        v-model="valData"
        :id="'checkbox-' + this.titleData"
        type="checkbox"
        class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded dark:bg-gray-700 dark:border-gray-600"
      />
      <label
        :for="'checkbox-' + this.titleData"
        class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300 capitalize"
      >
        {{ this.titleData }}
      </label>
    </div>

    <div v-else class="flex mb-4">
      <div class="flex items-center h-5">
        <input
          @change="changeCheckbox"
          v-model="valData"
          :id="'checkbox-' + this.titleData"
          aria-describedby="checkbox-symbols-text"
          type="checkbox"
          class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
        />
      </div>
      <div class="ms-2 text-sm">
        <label
          :for="'checkbox-' + this.titleData"
          class="font-medium text-gray-900 dark:text-gray-300 capitalize"
          >{{ this.titleData }}</label
        >
        <p
          :id="'checkbox-text-' + this.titleData"
          class="text-xs font-normal text-gray-500 dark:text-gray-400"
        >
          {{ this.detail }}
        </p>
      </div>
    </div>
  </div>
</template>
