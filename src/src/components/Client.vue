<template>
  <v-container>
    <h2 class="text-center">Regular Customer ?</h2>
    <div class="input">
      <v-text-field
        solo-inverted
        autofocus
        label="Enter Your Name"
        v-model="name"
        @keydown.enter="submit"
      >
      </v-text-field>
    </div>
  </v-container>
</template>

<style>
.input {
  width: 350px;
  position: absolute;
  margin-left: 700px;
  margin-top: 15px;
}
</style>

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
