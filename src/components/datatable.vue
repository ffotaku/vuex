<template>
  <div>
    <v-row no-gutters>
      <v-col md="4"><v-card class="pa-2 grey darken-3" outlined> id</v-card></v-col>
      <v-col md="4"><v-card class="pa-2 grey darken-3" outlined> price</v-card></v-col>
      <v-col md="4"><v-card class="pa-2 grey darken-3" outlined> date</v-card></v-col>
      

    </v-row>
    <v-row v-for="(items, index) in $store.getters.items" :key="index"  no-gutters>
      <v-col md="4"><v-card class="pa-2" outlined> {{ index + 1 }}</v-card></v-col>
      <v-col md="4"><v-card class="pa-2" outlined> {{ items.price }}</v-card></v-col>
      <v-col md="4"><v-card class="pa-2" outlined> {{ items.date }}</v-card></v-col>

      <td></td>
    </v-row>
    <v-btn class="mr-4" @click="page">add more</v-btn>
  </div>
</template>


<script>
export default {
  methods: {
    page() {
      this.$store.state.page = 1;
    },
  },
};
</script>

<style>
</style>