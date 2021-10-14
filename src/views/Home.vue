<template>
  <v-container>
    <div class="home container">
      <Header text="Resturant" />
      <Client @filterd-client="clientOrderFilter" :clients="clients" />
    </div>

    <div style="position:absolute; right:250px; top:150px;">
      <Firsts @add-to-order="addToOrder" :_firsts="firsts" />
    </div>
    <div>
      <Primary
        @primary-choosen="PrimaryChoosen"
        @add-to-order="addToOrder"
        :_primary="primary"
        style="position:absolute; right: 750px; top:150px;"
      />
    </div>
    <div style="position:absolute; left: 270px; top: 150px;">
      <Desserts
        :primaryChoosen="primaryChoosen"
        @add-to-order="addToOrder"
        :_desserts="desserts"
      />
    </div>
    <div>
      <OrderDetail
        @console-log-order="consolLogOrder"
        :validSend="validSend"
        :orders="orderdetail"
        class="pb-5"
        style="position:absolute; top: 900px;"
      />
    </div>
  </v-container>
</template>

<script>
import Header from "../components/Header";
import Firsts from "../components/Firsts";
import Primary from "../components/Primary";
import Desserts from "../components/Desserts";
import OrderDetail from "../components/OrderDetail";
import Client from "../components/Client";

export default {
  name: "Home",

  components: {
    Header,
    Firsts,
    Primary,
    Desserts,
    OrderDetail,
    Client,
  },

  data() {
    return {
      //Arrys

      firsts: [],
      primary: [],
      primaryChossenItems: [],
      desserts: [],
      orderdetail: [],
      clients: [],
      clientlimit: [],

      //Boolens
      primaryChoosen: false,
      validSend: false,
    };
  },

  //---- Creating the Connection to the DetaBase on Json-Server --Port:5000 ----//

  async created() {
    (this.firsts = await this.fetchFirsts()),
      (this.primary = await this.fetchPrimary()),
      (this.desserts = await this.fetchDesserts()),
      (this.clients = await this.fetchClients());
  },

  methods: {
    // ----- Retriving Data From Json-server DataBase ----//

    async fetchFirsts() {
      const res = await fetch("http://localhost:5000/firsts");
      const data = await res.json();
      return data;
    },
    async fetchPrimary() {
      const res = await fetch("http://localhost:5000/primary");
      const data = await res.json();
      return data;
    },
    async fetchDesserts() {
      const res = await fetch("http://localhost:5000/desserts");
      const data = await res.json();
      return data;
    },
    async fetchClients() {
      const res = await fetch("http://localhost:5000/clients");
      const data = await res.json();
      return data;
    },

    // ------- Filtering Menu acording to Redisterd Client --------- //

    clientOrderFilter(fClient, i, id) {
      id = 0;
      this.clientlimit = fClient;

      this.firsts.forEach((e) => {
        for (i = 0; i < this.clientlimit.length; i++) {
          if (e.name === this.clientlimit[i]) {
            id = e.id;
            this.firsts[id].disabled = true;
          }
        }
      });

      this.primary.forEach((e) => {
        for (i = 0; i < this.clientlimit.length; i++) {
          if (e.name === this.clientlimit[i]) {
            id = e.id;
            this.primary[id].disabled = true;
          }
        }
      });

      this.desserts.forEach((e) => {
        for (i = 0; i < this.clientlimit.length; i++) {
          if (e.name === this.clientlimit[i]) {
            id = e.id;
            this.desserts[id].disabled = true;
          }
        }
      });
    },

    // --- Adding Order By Clicking the "+" icon ---//

    addToOrder(item) {
      this.orderdetail.push(item);
      this.validSend = true;
      console.log(this.orderdetail);
    },

    // ------ Enabeling Access to Dessert Menu and Informing the Desert Ui acording to Demands ---- //

    PrimaryChoosen(pItem) {
      this.primaryChossenItems.push(pItem);
      this.primaryChoosen = true;
      this.dessertsLimitiation();
    },

    // --- limiting the Desserts View Acording to Primary Picks --- //

    dessertsLimitiation() {
      if (
        this.primaryChossenItems.includes("tortia") ||
        this.primaryChossenItems.includes("fried chiken")
      ) {
        this.desserts[3].disabled = true;
      }
      if (
        this.primaryChossenItems.includes("pizza") ||
        this.primaryChossenItems.includes("stake")
      ) {
        this.desserts[2].disabled = true;
      }
    },
    consolLogOrder() {
      console.log(
        "Your Orders Are: ",
        this.orderdetail,
        "Total amount :",
        this.orderdetail.length
      );
    },
  },
};
</script>
