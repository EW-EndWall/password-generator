<script>
export default {
  name: "Button",
  props: {
    changeConfig: Function,
  },
};
</script>

<template>
  <div>
    <button
      @click="changeConfig"
      type="submit"
      class="block mx-auto text-white bg-blue-700 hover:bg-blue-800 focus:outline-none font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 mb-4"
    >
      Refresh
    </button>
  </div>
</template>
