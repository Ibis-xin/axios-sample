<template>
  <div>
    <div v-for="bill in bills" :key="bill.id">
      <table width="100%">
        <tr>
          <td>purchaser</td>
          <td>{{ bill.purchaser }}</td>
        </tr>
        <tr>
          <td>phone</td>
          <td>{{ bill.phone }}</td>
        </tr>
        <tr>
          <td>other</td>
          <td>{{ bill.other }}</td>
        </tr>
        <tr>
          <td>creationDateTime</td>
          {{
            bill.creationDateTime
          }}
          <td></td>
        </tr>
        <tr>
          <td>checkOutDateTime</td>
          {{
            bill.checkOutDateTime
          }}
          <td></td>
        </tr>
        <tr v-for="project in bill.projectList" :key="project.index">
          <td>projectList</td>
          <td>{{ project }}</td>
        </tr>
      </table>
    </div>
    <button @click="getBills()">Get</button>
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
      bills: [
        {
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
          id: "",
          checkOutDateTime: "2021-11-13T03:05:27.075Z",
        },
      ],
    };
  },
  methods: {
    getBills() {
      console.log(localStorage.getItem("token"));
      axios
        .get("https://localhost:44301/Record/GetBills", {
          headers: { Authorization: `Bearer ${localStorage.getItem("token")}` },
        })
        .then((response) => {
          for (let i = 0; i < response.data.length; i++) {
            this.$set(this.bills, i, response.data[i]);
          }
        })
        .catch(() => console.log("Get Bills Fail."));
    },
  },
};
</script>

<style>
</style>