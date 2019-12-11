<template>
  <div>
    <!-- <br />
    <br />
    <v-card color="info" dark outlined>
      <hr />
      <center>
        <h1>Pending Requests</h1>
      </center>
      <hr />
    </v-card> -->
 
      <RequestTable
        
        :request="requests"
        @remove="removeItem(request)"
      />

  </div>
</template>
<script>
import RequestTable from "../modules/tibs/RequestTable.vue";
import { getPending } from "../actions/requestAxios.js";
// import io from "socket.io-client";
// var socket = io.connect("http://localhost:3232");
export default {
  components: {
    RequestTable
  },
  data() {
    return {
      sample: "sample",
      username: "redgie",
      requests: [{
         firstnname: 'Renzy',
          lastname: 'Verano',
          category: "Personal",
          when: "2019-12-15",
          batch: 2021,
      }]
    };
  },
  methods: {
    removeItem(request) {
      this.requests.splice(this.requests.indexOf(request), 1);
    }
  },
  mounted() {
    getPending()
      .then(data => (this.requests = data.data))
      .catch(err => alert(err));
  }
};
</script>
