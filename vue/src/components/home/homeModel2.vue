<script setup>
import { ref } from "vue";

const checkLength = ref();

const checkLengthText = ref();
const checkUppercase = ref();
const checkLowercase = ref();
const checkNumbers = ref();
const checkSymbols = ref();
</script>

<script>
export default {
  name: "Home",
  data() {
    return {
      passwordData: "",
    };
  },
  computed: {
    resultPassword() {
      return this.passwordData;
    },
  },
  mounted() {
    this.$refs.checkLength.value = this.$refs.checkLengthText.innerText = 32;

    this.$refs.checkUppercase.checked = true;
    this.$refs.checkLowercase.checked = true;
    this.$refs.checkNumbers.checked = false;
    this.$refs.checkSymbols.checked = false;

    this.changeConfig();
  },
  methods: {
    changeRange(event) {
      this.$refs.checkLengthText.innerText = event.target.value;
      this.changeConfig();
    },

    changeConfig() {
      const length = this.$refs.checkLength.value;
      const type = [];
      const refNames = [
        "checkUppercase",
        "checkLowercase",
        "checkNumbers",
        "checkSymbols",
      ];
      refNames.forEach((refName) => {
        if (this.$refs[refName].checked) {
          type.push(refName);
        }
      });
      const password = this.generatePassword({ length, typeData: type });
      this.passwordData = password;
    },

    generatePassword(data) {
      const { length, typeData } = data;

      let charset = "";
      let password = "";

      typeData.map((item) => {
        if (item == "checkUppercase") charset += "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        if (item == "checkLowercase") charset += "abcdefghijklmnopqrstuvwxyz";
        if (item == "checkNumbers") charset += "0123456789";
        if (item == "checkSymbols") charset += `"'!@#$%^&*`;
      });

      for (var i = 0; i < length; i++) {
        const randomIndex = Math.floor(Math.random() * charset.length);
        password += charset[randomIndex];
      }
      return password;
    },
  },
};
</script>

<template>
  <div class="m-8">
    <div class="container mx-auto border-x-4 rounded-xl p-4 shadow-xl">
      <div class="relative z-0 w-full mb-5 group">
        <input
          type="text"
          name="floating_password"
          id="floating_password"
          class="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
          placeholder=" "
          :value="resultPassword"
        />
        <label
          for="floating_password"
          class="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:start-0 rtl:peer-focus:translate-x-1/4 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
          >Password</label
        >
      </div>

      <fieldset>
        <div class="text-center" ref="checkLengthText"></div>
        <div class="relative mb-8">
          <label for="labels-range-input-nummber" class="sr-only"
            >Labels range</label
          >
          <input
            @input="changeRange"
            id="labels-range-input-nummber"
            type="range"
            value="16"
            min="4"
            max="64"
            class="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer dark:bg-gray-700"
            ref="checkLength"
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
        <div class="flex items-center mb-4">
          <input
            @change="changeConfig"
            id="checkbox-uppercase"
            type="checkbox"
            value=""
            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
            ref="checkUppercase"
          />
          <label
            for="checkbox-uppercase"
            class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300"
            >Uppercase</label
          >
        </div>
        <div class="flex items-center mb-4">
          <input
            @change="changeConfig"
            id="checkbox-lowercase"
            type="checkbox"
            value=""
            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
            ref="checkLowercase"
          />
          <label
            for="checkbox-lowercase"
            class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300"
            >Lowercase</label
          >
        </div>
        <div class="flex items-center mb-4">
          <input
            @change="changeConfig"
            id="checkbox-numbers"
            type="checkbox"
            value=""
            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
            ref="checkNumbers"
          />
          <label
            for="checkbox-numbers"
            class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300"
            >Numbers</label
          >
        </div>

        <div class="flex mb-4">
          <div class="flex items-center h-5">
            <input
              @change="changeConfig"
              id="checkbox"
              aria-describedby="checkbox-symbols-text"
              type="checkbox"
              value=""
              class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
              ref="checkSymbols"
            />
          </div>
          <div class="ms-2 text-sm">
            <label
              for="checkbox-symbols"
              class="font-medium text-gray-900 dark:text-gray-300"
              >Symbols</label
            >
            <p
              id="checkbox-symbols-text"
              class="text-xs font-normal text-gray-500 dark:text-gray-400"
            >
              ( !@#$%^&* )
            </p>
          </div>
        </div>
      </fieldset>
    </div>
  </div>
</template>
