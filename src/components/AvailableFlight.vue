<template>
  <div class="flight-container">
    <b-nav tabs>
      <b-nav-item active>Available Flight</b-nav-item>
      <b-nav-item>Filter By Price</b-nav-item>
      <b-nav-item>Filter By Time</b-nav-item>
    </b-nav>

    <b-card-group class="card-grp">
      <b-card class="flight">
        <b-table
          striped
          hover
          :items="items.slice(1, 5)"
          :fields="fields"
        ></b-table>
      </b-card>

      <b-card class="flight">
        <b-card-text>
          <!--
         <div>
    <ul v-if="posts && posts.length">
      <li v-for="post of posts.slice(1,5)" :key="post.title">
        <p><strong>{{post.title}}</strong></p>
        <p>{{post.body}}</p>
      </li>
    </ul>
    <p v-if="!posts">
      ...Loading...
     </p>
    <ul v-if="errors && errors.length">
      <li v-for="error of errors" :key="error.message">
        {{error.message}}
      </li>
    </ul>
  </div>
  -->
        </b-card-text>
      </b-card>
      <b-card class="flight">
        <b-card-text>
          <p>Reboot and Refund</p>
          <font-awesome-icon style="font-size:28px;" icon="user-secret" />
        </b-card-text>
      </b-card>
    </b-card-group>
    <b-card-group>
      <b-card class="f-card">
        <b-card-text>
          <p>Manage Booking</p>
          <font-awesome-icon style="font-size:28px" icon="user-secret" />
        </b-card-text>
      </b-card>

      <b-card class="f-card">
        <b-card-text>
          <p>Check In</p>
          <font-awesome-icon style="font-size:28px" icon="user-secret" />
        </b-card-text>
      </b-card>
      <b-card class="f-card">
        <b-card-text>
          <p>Reboot and Refund</p>
          <font-awesome-icon style="font-size:28px;" icon="user-secret" />
        </b-card-text>
      </b-card>
      <b-card class="f-card">
        <b-card-text>
          <p>Covid 19 Updates</p>
          <font-awesome-icon style="font-size:28px" icon="user-secret" />
        </b-card-text>
      </b-card>
    </b-card-group>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Flight",
  data() {
    return {
      flughtData: [],
      posts: [],
      errors: [],
      items: [
        {
          isActive: true,
          age: 40,
          first_name: "Dickerson",
          last_name: "Macdonald"
        },
        { isActive: false, age: 21, first_name: "Larsen", last_name: "Shaw" },
        { isActive: false, age: 89, first_name: "Geneva", last_name: "Wilson" },
        { isActive: true, age: 38, first_name: "Jami", last_name: "Carney" }
      ]
    };
  },
  /*
  fetch data from api
  */
  created() {
    /*
    axios.get(`http://jsonplaceholder.typicode.com/posts`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
    this.post=this.post.slice(1,10)
    
  }
  */
    /*
  fetch flight data
  */
    axios
      .get(
        `https://api.sharetrip.net/api/v1/flight/search?tripType=Return&adult=1&child=0&infant=0&class=Economy&origin=DAC&destination=DXB&depart=2021-12-25&depart=2021-12-30`
      )
      .then(response => {
        // JSON responses are automatically parsed.
        //this.posts = response.data;
        response = JSON.stringify(response);
        //const d=response.data.response.flights[0].flight[1].originName;
        response = JSON.parse(response);
        const originCity =
          response.data.response.flights[0].flight[0].originName.city;
        const destinationCity =
          response.data.response.flights[0].flight[0].destinationName.city;
        const originCode =
          response.data.response.flights[0].flight[0].originName.code;
        const destinationCode =
          response.data.response.flights[0].flight[0].destinationName.code;
        const arivalTime =
          response.data.response.flights[0].flight[0].arrivalDateTime.time;
        const departureTime =
          response.data.response.flights[0].flight[0].departureDateTime.time;
        const durationTime =
          response.data.response.flights[0].flight[0].duration;
        console.log(
          "data is : " +
            originCity +
            " destination name : " +
            destinationCity +
            " origin code : " +
            originCode +
            " destination Code : " +
            destinationCode +
            " Arrival time is : " +
            arivalTime +
            " departure time : " +
            departureTime+
            " Duration : "+durationTime
        );
        const eachFlight={
          originCity:originCity,
          destinationCity:destinationCity,
          originCode :originCode,
          destinationCode:destinationCode,
          arivalTime:arivalTime,
          departureTime:departureTime,


        };
    
        console.log("Flight one info is : "+eachFlight)
        //response=JSON.parse(response)
        //console.log("D is : "+d)

        //console.log("Data is  : ")
      })
      .catch(e => {
        this.errors.push(e);
      });
    this.post = this.post.slice(1, 10);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Abril+Fatface&display=swap");
.flight-container .card-grp {
  margin-right: 20px 20px 20px 80px;
}
</style>
