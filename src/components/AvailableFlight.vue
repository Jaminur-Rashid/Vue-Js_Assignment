<template>
  <div class="flight-container">
    <b-nav tabs>
      <b-nav-item active>Available Flight</b-nav-item>
      <b-nav-item v-if="flightData !== undefined" v-on:click="sortUsingPrice"
        >Filter By Price</b-nav-item
      >
      <b-nav-item v-on:click="sortUsingTime">Filter By Time</b-nav-item>
    </b-nav>
    <div class="flight-table">
      <li
        style="list-style-type: none;"
        v-for="post of flightData"
        v-if="
          flightData !== undefined &&
            sortByPrice === false &&
            sortByTime === false
        "
      >
        <b-card style="margin:5px 100px 0px 100px;border-left:2px solid pink">
          <b-row>
            <b-col style="text-align:center;">
              <h6>{{ post.arivalTime }}</h6>
              <p>{{ post.originCode }}</p>
            </b-col>
            <b-col style="text-align:center;">
              <img
                style="height:20px;width:20px;color:blue;"
                src="https://i.ibb.co/Xp52K8D/plane-solid.png"
                alt="plane-solid"
                border="0"
              />
              <p>{{ post.durationTime }}</p>
            </b-col>
            <b-col style="text-align:center;">
              <h6>{{ post.departureTime }}</h6>
              <p>{{ post.destinationCity }}</p>
            </b-col>
            <b-col style="text-align:center;">
              <h6>{{ post.price }}</h6>
            </b-col>
          </b-row>
        </b-card>
      </li>
    </div>
    <div class="flight-table">
      <li
        style="list-style-type: none;"
        v-for="post of flightData"
        v-if="
          flightData !== undefined &&
            sortByPrice === true &&
            sortByTime === false
        "
      >
        <b-card style="margin:5px 100px 0px 100px;border-left:2px solid pink">
          <b-row>
            <b-col style="text-align:center;">
              <h6>{{ post.arivalTime }}</h6>
              <p>{{ post.originCode }}</p>
            </b-col>
            <b-col style="text-align:center;">
              <img
                style="height:20px;width:20px;color:blue;"
                src="https://i.ibb.co/Xp52K8D/plane-solid.png"
                alt="plane-solid"
                border="0"
              />
              <p>{{ post.durationTime }}</p>
            </b-col>
            <b-col style="text-align:center;">
              <h6>{{ post.departureTime }}</h6>
              <p>{{ post.destinationCity }}</p>
            </b-col>
            <b-col style="text-align:center;">
              <h1>{{ post.price }}</h1>
            </b-col>
          </b-row>
        </b-card>
      </li>
    </div>
    <div class="flight-table">
      <li
        style="list-style-type: none;"
        v-for="post of flightData"
        v-if="
          flightData !== undefined &&
            sortByPrice === false &&
            sortByTime === true
        "
      >
        <b-card style="margin:5px 100px 0px 100px;border-left:2px solid pink">
          <b-row>
            <b-col style="text-align:center;">
              <h6>{{ post.arivalTime }}</h6>
              <p>{{ post.originCode }}</p>
            </b-col>
            <b-col style="text-align:center;">
              <img
                style="height:20px;width:20px;color:blue;"
                src="https://i.ibb.co/Xp52K8D/plane-solid.png"
                alt="plane-solid"
                border="0"
              />
              <p>{{ post.durationTime }}</p>
            </b-col>
            <b-col style="text-align:center;">
              <h6>{{ post.departureTime }}</h6>
              <p>{{ post.destinationCity }}</p>
            </b-col>
            <b-col style="text-align:center;">
              <h1>{{ post.price }}</h1>
            </b-col>
          </b-row>
        </b-card>
      </li>
    </div>
    <div>
      <!--
      <b-card>
        <b-table
          v-if="
            flightData !== undefined &&
              sortByPrice === false &&
              sortByTime === false
          "
          striped
          hover
          :items="flightData"
        ></b-table
      ></b-card>
      
      <b-table
        v-if="flightData !== undefined && sortByTime === true"
        striped
        hover
        :items="flightData"
      ></b-table>
      -->
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Flight",
  data() {
    return {
      isOk: 0,
      flightData: [],
      sortByTime: false,
      sortByPrice: false,
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
  methods: {
    /*
  Method to sort flight by price
  */
    sortUsingPrice: function() {
      this.sortByTime = false;
      alert("flightDta");
      this.flightData.sort(function(a, b) {
        return a.price - b.price;
      });
      this.sortByPrice = true;
    },
    /*
    method to sort flight using time 
    */
    sortUsingTime: function() {
      this.sortByPrice = false;
      alert("flightDta");
      this.flightData.sort(function(a, b) {
        return a.arivalTime.localeCompare(b.arivalTime);
      });
      this.sortByTime = true;
    }
  },
  /*
  fetch data from api
  */
  created() {
    axios
      .get(
        `https://api.sharetrip.net/api/v1/flight/search?tripType=Return&adult=1&child=0&infant=0&class=Economy&origin=DAC&destination=DXB&depart=2021-12-25&depart=2021-12-30`
      )
      .then(response => {
        // JSON responses are automatically parsed.
        //this.posts = response.data;
        response = JSON.stringify(response);
        console.log(response);
        //const d=response.data.response.flights[0].flight[1].originName;
        response = JSON.parse(response);
        let counterValue = 0;
        let allFlightsData = [];
        let flightPrices = [
          9876,
          2342,
          1947,
          10000,
          45000,
          5000,
          3333,
          7654,
          12345,
          6567
        ];
        const flightsLength = response.data.response.flights.length;
        console.log("Total Flights : " + flightsLength);
        try {
          for (let i = 0; i < flightsLength; i++) {
            // console.log("It works"+response.data.response.flights[1].flight[i].originName.city );
            //console.log(typeof(flightsArr[i].flight[i].destinationName.city))
            const originCity =
              response.data.response.flights[i].flight[0].originName.city;
            const originAirport =
              response.data.response.flights[i].flight[0].originName.airport;
            const destinationCity =
              response.data.response.flights[i].flight[0].destinationName.city;
            const originCode =
              response.data.response.flights[i].flight[0].originName.code;
            const destinationAirport =
              response.data.response.flights[i].flight[0].destinationName
                .airport;
            const destinationCode =
              response.data.response.flights[i].flight[0].destinationName.code;
            const arivalTime =
              response.data.response.flights[i].flight[0].arrivalDateTime.time;
            const departureTime =
              response.data.response.flights[i].flight[0].departureDateTime
                .time;
            const durationTime =
              response.data.response.flights[i].flight[0].duration;
            const logo = response.data.response.flights[i].flight[0].logo;
            console.log("data slicing done");
            const eachFlight = {
              originCity: originCity,
              destinationCity: destinationCity,
              originCode: originCode,
              destinationCode: destinationCode,
              arivalTime: arivalTime,
              departureTime: departureTime,
              originAirport: originAirport,
              destinationAirport: destinationAirport,
              price: flightPrices[i],
              durationTime: durationTime,
              logo: logo
            };
            console.log("Creating flight object is done");
            allFlightsData.push(eachFlight);
            console.log("Pushing data is done");

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
                departureTime +
                " Duration : " +
                durationTime
            );

            console.log("Origin name is : " + originCity);
            counterValue++;
          }
        } catch (error) {
          console.log("Error" + error.message);
        }
        console.log("# Debug Conter value : " + counterValue);
        //console.log("Flight one info is : "+allFlightsData[0].originCity)
        for (let i = 0; i < flightsLength; i++) {
          console.log(
            " Flight " +
              i +
              " Info is " +
              " origin " +
              allFlightsData[i].originCity +
              " destination city " +
              allFlightsData[i].destinationCity +
              " origin code " +
              allFlightsData[i].originCode +
              " destination code " +
              allFlightsData[i].destinationCode +
              " Arrival time " +
              allFlightsData[i].arivalTime +
              " Departure time : " +
              allFlightsData[i].departureTime +
              " origin airport : " +
              allFlightsData[i].originAirport +
              " destination airport : " +
              allFlightsData[i].destinationAirport +
              " Price : " +
              allFlightsData[i].price
          );
        }
        this.flightData = allFlightsData;
        console.log(this.flightData);
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Abril+Fatface&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Rubik+Mono+One&display=swap");

.flight-container .card-grp {
  margin-right: 20px 20px 20px 80px;
}
/*
style flight table
*/
.flight-container .flight-table h6 {
  /*text-align: left;*/
  font-family: "Rubik Mono One", sans-serif;
  color: teal;
  font-size: 12px;
}
.flight-container .flight-table p {
  font-family: "Roboto", sans-serif;
  color: black;
  font-size: 10px;
}
.flight-container .flight-table h1 {
  font-family: "Roboto", sans-serif;
  color: black;
  font-size: 10px;
  margin-top: 20px;
}
.flight-container .flight-table {
  background-color: #e6e6e6;
  font-family: "Rubik Mono One", sans-serif;
  /*color:teal;**/
}
.flight-table .price-btn {
  background-color: #07457e;
  color: #ffffff;
  border: none;
  width: 80px;
}
</style>
