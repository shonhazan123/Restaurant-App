<template>
  <v-card class="mx-auto my-12" max-width="374">
    <v-card-title class="justify-center">Firsts</v-card-title>
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
            <tr v-for="item in _firsts" :key="item.id">
              <td>{{ item.name }}</td>
              <v-btn
                v-if="!item.disabled"
                @click="$emit('add-to-order', item.name)"
                rounded
                style="postion:absoulut; left: 40px;"
                text
                icon
                color="blue lighten-2"
              >
                <v-icon>mdi-plus</v-icon>
              </v-btn>
              <v-btn v-else rounded style="postion:absoulut; left: 40px;" icon>
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
  name: "Firsts",

  props: {
    _firsts: Array,
  },
};
</script>
