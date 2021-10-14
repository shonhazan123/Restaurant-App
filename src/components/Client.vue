<template>
  <v-container>
    <h2 class="text-center">Regular Customer ?</h2>
    <v-text-field
      label="Enter Your Name"
      v-model="name"
      @keydown.enter="submit"
    >
    </v-text-field>
  </v-container>
</template>

<script>
export default {
  name: "Client",
  props: {
    clients: Array,
  },
  data() {
    return {
      name: "",
      filterdClient: [],
      limits: [],
    };
  },
  methods: {
    submit() {
      this.clients.forEach((element) => {
        element.name.toLowerCase() === this.name.toLowerCase()
          ? this.filterdClient.push(element)
          : this.filterdClient;
      });
      if (this.filterdClient) {
        this.limits = this.filterdClient[0].limit;
        this.$emit("filterd-client", this.limits);
      }
    },
  },
};
</script>
