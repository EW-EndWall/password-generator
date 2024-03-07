<script>
import componentButton from "./button.vue";
import componentPassword from "./password.vue";
import componentLength from "./length.vue";
import componentCheckbox from "./checkbox.vue";

export default {
  name: "Home",
  components: {
    componentButton,
    componentPassword,
    componentLength,
    componentCheckbox,
  },
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
      this.generateConfig.length = Number(event); // * set password length
    },
    // * option change
    changeCheckbox(data) {
      const { typeData } = this.generateConfig;
      // * set uppercase config
      typeData[data[0]] = data[1];
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
      <componentPassword :resultPassword="resultPassword" />

      <componentButton :changeConfig="changeConfig" />

      <fieldset>
        <componentLength
          :changeConfig="changeConfig"
          :length="generateConfig.length"
          @length-data="changeRange"
        />

        <componentCheckbox
          :titleData="'uppercase'"
          :valueData="generateConfig.typeData.uppercase"
          :changeConfig="changeConfig"
          @change-checkbox="changeCheckbox"
        />

        <componentCheckbox
          :titleData="'lowercase'"
          :valueData="generateConfig.typeData.lowercase"
          :changeConfig="changeConfig"
          @change-checkbox="changeCheckbox"
        />

        <componentCheckbox
          :titleData="'numbers'"
          :valueData="generateConfig.typeData.number"
          :changeConfig="changeConfig"
          @change-checkbox="changeCheckbox"
        />
        <componentCheckbox
          :titleData="'symbols'"
          :valueData="generateConfig.typeData.symbols"
          :changeConfig="changeConfig"
          :detail="'( !@#$%^&* )'"
          @change-checkbox="changeCheckbox"
        />
      </fieldset>
    </div>
  </div>
</template>
