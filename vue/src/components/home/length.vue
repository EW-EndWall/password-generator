<script>
export default {
  name: "Length",
  props: {
    changeConfig: Function,
    length: Number,
  },
  data() {
    return {
      lengthData: this.length,
    };
  },
  methods: {
    // * change range data
    changeRange(event) {
      this.$emit("length-data", this.lengthData);
      // * generate password
      this.changeConfig();
    },
  },
};
</script>

<template>
  <div>
    <div class="text-center">{{ this.lengthData }}</div>
    <div class="relative mb-8">
      <label for="labels-range-input-nummber" class="sr-only"
        >Labels range</label
      >
      <input
        @input="changeRange"
        v-model="this.lengthData"
        id="labels-range-input-nummber"
        type="range"
        min="4"
        max="64"
        class="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer dark:bg-gray-700"
      />
      <span
        class="text-sm text-gray-500 dark:text-gray-400 absolute start-0 -bottom-6"
      >
        4
      </span>
      <span
        class="text-sm text-gray-500 dark:text-gray-400 absolute end-0 -bottom-6"
      >
        64
      </span>
    </div>
  </div>
</template>
