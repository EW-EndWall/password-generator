<script>
export default {
  name: "Home",
  data() {
    return {
      passwordData: "",
      generateConfig: {
        length: 16,
        typeData: {
          uppercase: true,
          lowercase: true,
          numbers: false,
          symbols: false,
        },
      },
    };
  },
  mounted() {
    // * first create password
    this.changeConfig();
  },
  computed: {
    // * password content
    resultPassword() {
      return this.passwordData;
    },
  },
  methods: {
    // * change range data
    changeRange(event) {
      // * set password length
      this.generateConfig.length = event.target.value;
      this.changeConfig();
    },
    // * change uppercase data
    changeUppercase(event) {
      const { typeData } = this.generateConfig;
      // * set uppercase config
      typeData.uppercase = event.target.checked;
      // * generate password
      this.changeConfig();
    },
    // * change lowercase data
    changeLowercase(event) {
      const { typeData } = this.generateConfig;
      // * set lowercase config
      typeData.lowercase = event.target.checked;
      // * generate password
      this.changeConfig();
    },
    // * change numbers data
    changeNumbers(event) {
      const { typeData } = this.generateConfig;
      // * set numbers config
      typeData.numbers = event.target.checked;
      // * generate password
      this.changeConfig();
    },
    // * change symbols data
    changeSymbols(event) {
      const { typeData } = this.generateConfig;
      // * set symbols config
      typeData.symbols = event.target.checked;
      // * generate password
      this.changeConfig();
    },
    // * change config data
    changeConfig() {
      const { length, typeData } = this.generateConfig;
      // * filter password content to be generated
      const type = Object.keys(typeData).filter((key) => typeData[key]);
      const password = this.generatePassword({ length, typeData: type });
      // * set password
      this.passwordData = password;
    },
    // * generate password
    generatePassword(data) {
      const { length, typeData } = data;

      let charset = "";
      let password = "";
      // * password content
      typeData.map((item) => {
        if (item == "uppercase") charset += "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        if (item == "lowercase") charset += "abcdefghijklmnopqrstuvwxyz";
        if (item == "numbers") charset += "0123456789";
        if (item == "symbols") charset += `"'!@#$%^&*`;
      });
      // * random sellect
      for (let i = 0; i < length; i++) {
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
        <label
          for="email-address-icon"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >Password</label
        >
        <div class="relative">
          <div
            class="absolute inset-y-0 start-0 flex items-center ps-3.5 pointer-events-none"
          >
            <svg
              class="w-4 h-4"
              stroke="currentColor"
              fill="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M18 8H20C20.5523 8 21 8.44772 21 9V21C21 21.5523 20.5523 22 20 22H4C3.44772 22 3 21.5523 3 21V9C3 8.44772 3.44772 8 4 8H6V7C6 3.68629 8.68629 1 12 1C15.3137 1 18 3.68629 18 7V8ZM5 10V20H19V10H5ZM11 14H13V16H11V14ZM7 14H9V16H7V14ZM15 14H17V16H15V14ZM16 8V7C16 4.79086 14.2091 3 12 3C9.79086 3 8 4.79086 8 7V8H16Z"
              ></path>
            </svg>
          </div>
          <input
            type="text"
            id="email-address-icon"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full ps-10 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            :value="resultPassword"
            readonly
          />
        </div>
      </div>

      <button
        @click="changeConfig"
        type="submit"
        class="block mx-auto text-white bg-blue-700 hover:bg-blue-800 focus:outline-none font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 mb-4"
      >
        Refresh
      </button>

      <fieldset>
        <div class="text-center">{{ this.generateConfig.length }}</div>
        <div class="relative mb-8">
          <label for="labels-range-input-nummber" class="sr-only"
            >Labels range</label
          >
          <input
            @input="changeRange"
            v-model="generateConfig.length"
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
        <div class="flex items-center mb-4">
          <input
            @change="changeUppercase"
            v-model="generateConfig.typeData.uppercase"
            id="checkbox-uppercase"
            type="checkbox"
            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
          />
          <label
            for="checkbox-uppercase"
            class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300"
            >Uppercase</label
          >
        </div>
        <div class="flex items-center mb-4">
          <input
            @change="changeLowercase"
            v-model="generateConfig.typeData.lowercase"
            id="checkbox-lowercase"
            type="checkbox"
            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
          />
          <label
            for="checkbox-lowercase"
            class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300"
            >Lowercase</label
          >
        </div>
        <div class="flex items-center mb-4">
          <input
            @change="changeNumbers"
            v-model="generateConfig.typeData.number"
            id="checkbox-numbers"
            type="checkbox"
            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
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
              @change="changeSymbols"
              v-model="generateConfig.typeData.symbols"
              id="checkbox"
              aria-describedby="checkbox-symbols-text"
              type="checkbox"
              class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
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
