<template>
  <div>
    <span>purchaser: </span>
    <input v-model="bill.purchaser" />
    <br />

    <span>phone: </span>
    <input v-model="bill.phone" />
    <br />

    <span>other: </span>
    <input v-model="bill.other" />
    <br />

    <div>projectList:</div>
    <div>
      <span>name: </span>
      <input v-model="bill.projectList[0].name" />
      <br />
      <span>unitPrice: </span>
      <input v-model="bill.projectList[0].unitPrice" />
      <br />
      <span>quantity: </span>
      <input v-model="bill.projectList[0].quantity" />
      <br />
      <span>remark: </span>
      <input v-model="bill.projectList[0].remark" />
      <br />
    </div>

    <button @click="sendBill()">Send</button>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios);

export default {
  data() {
    return {
      bill: {
        purchaser: "",
        phone: "",
        creationDateTime: "",
        projectList: [
          {
            name: "",
            unitPrice: 0,
            quantity: 0,
            remark: "",
          },
        ],
        other: "",
      },
    };
  },
  methods: {
    sendBill() {
      this.bill.creationDateTime = Date.now;
      axios
        .post("https://localhost:44301/Record/insertBill", this.bill,{
          headers: { Authorization: `Bearer ${localStorage.getItem("token")}` },
        })
        .then((response) => {
          console.log(response.data);
        })
        .catch((response) => {
          console.log(response.data);
        });
    },
  },
};
</script>

<style>
</style>