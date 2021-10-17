<template>
  <v-card class="mx-auto my-12" max-width="374">
    <v-card-title class="justify-center">Desserts</v-card-title>
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img
      height="250"
      src="https://cdn.vuetifyjs.com/images/cards/cooking.png"
    ></v-img>

    <v-card>
      <v-simple-table>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">
                Name
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in _desserts" :key="item.id">
              <td>{{ item.name }}</td>
              <v-btn
                v-if="primaryChoosen && !clicked && !item.disabled"
                @click="onClick(item.name)"
                text
                icon
                color="green lighten-2"
              >
                <v-icon>mdi-plus</v-icon>
              </v-btn>
              <v-btn
                v-else-if="clicked || (item.disabled && primaryChoosen)"
                icon
                disabled
              >
                <v-icon>mdi-plus</v-icon>
              </v-btn>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-card>
  </v-card>
</template>

<script>
export default {
  name: "Desserts",
  props: {
    _desserts: Array,
    primaryChoosen: Boolean,
  },
  data() {
    return {
      clicked: false,
    };
  },
  methods: {
    onClick(Item) {
      this.clicked = true;
      this.$emit("add-to-order", Item);
    },
  },
};
</script>
