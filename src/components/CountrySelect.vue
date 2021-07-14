<template>
  <div class="w-full grid justify-center">
    <select
      @change="onChange()"
      v-model="selected"
      class="form-select mb-10 border p-3 rounded"
    >
      <option value="Global">Global</option>
      <option v-for="country in countries" :value="country.ID">
        {{ country.Country }}
      </option>
    </select>
  </div>
</template>


<script>
export default {
  name: "CountrySelect",
  props: ["countries"],
  data() {
    return {
      selected: "Global",
    };
  },

  methods: {
    onChange() {
      if (this.selected !== "Global") {
        const country = this.countries.find(
          (item) => item.ID === this.selected
        );
        this.$emit("get-country", country);
      } else {
        this.$emit("set-global");
      }
    },
  },
};
</script>