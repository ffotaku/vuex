<template>
  <div>
    <v-form ref="form" v-model="valid" lazy-validation>
    <v-text><h1> Transfer of evidence</h1></v-text>
      <v-menu
        ref="menu"
        v-model="menu"
        :close-on-content-click="false"
        transition="scale-transition"
        offset-y
        min-width="290px"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="date"
            label="Pay date"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          ref="picker"
          v-model="date"
          :max="new Date().toISOString().substr(0, 10)"
          min="1950-01-01"
          @change="save"
        ></v-date-picker>
      </v-menu>
      <v-text-field
        v-model="price"
        type="number"
        style="1"
        label="price"
        required
      ></v-text-field>
      <v-file-input
        label="File input"
        v-model="img"
        filled
        prepend-icon="mdi-camera"
      ></v-file-input>
      <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
        Validate
      </v-btn>
      <v-btn color="error" class="mr-4" @click="reset"> Reset Form </v-btn>
      <v-btn class="mr-4" @click="page">See all</v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    name: "",
    status: "",
    price: "",
    select: null,
    img: null,
    date: null,
    menu: false,
  }),
  watch: {
    menu(val) {
      val && setTimeout(() => (this.$refs.picker.activePicker = "YEAR"));
    },
  },
  methods: {
    validate() {
      if (this.date) {
        let payload = {
          price: this.price,
          img: this.img,
          date: this.date
        };
        this.$store.dispatch("setItem", payload);
      }
    },
    reset() {
      this.$refs.form.reset();
    },
    page() {
      this.$store.state.page = 2;
    },
    save(date) {
      this.$refs.menu.save(date);
    },
  },
};
</script>

<style>
</style>