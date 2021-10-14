<template>
  <v-container>
    <v-row justify="space-around">
      <v-card width="400">
        <v-app-bar flat color="rgba(0, 0, 0, 0)">
          <v-app-bar-nav-icon color="white"></v-app-bar-nav-icon>
          <v-toolbar-title class="text-h6 black--text pl-0">
            Order Detail
          </v-toolbar-title>

          <v-btn color="white" icon>
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </v-app-bar>
        <v-card-text v-if="!validSend">
          <div class="font-weight-bold ml-8 mb-2">
            Must Add Items
            <v-btn disabled style="left: 50%; transform: translateX(-50%)"
              >Send!</v-btn
            >
          </div>
        </v-card-text>

        <v-card-text v-if="validSend">
          <div class="font-weight-bold ml-8 mb-2">
            <span>Orders</span>
          </div>

          <v-timeline align-top dense>
            <v-timeline-item v-for="order in orders" :key="order">
              <div>
                <div class="font-weight-normal">
                  <strong>{{ order }}</strong>
                </div>
              </div>
            </v-timeline-item>
          </v-timeline>
        </v-card-text>
        <v-btn
          @click="$emit('console-log-order')"
          v-if="validSend"
          style="left: 50%; transform: translateX(-50%)"
          color="green"
          >Send!</v-btn
        >
      </v-card>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "OrderDetail",
  props: {
    orders: Array,
    validSend: Boolean,
  },
  data() {
    return {
      orderNum: 0,
    };
  },
};
</script>
