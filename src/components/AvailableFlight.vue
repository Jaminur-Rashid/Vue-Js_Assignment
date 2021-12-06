<template>
  <div class="flight-container">
    <!--
    Test start
    --->
    <div>
      <div>
        <b-card body-class="text-center" header-tag="nav">
          <template #header>
            <b-nav card-header tabs>
              <b-nav-item active style="color:purple;font-weight:900"
                >Flight</b-nav-item
              >
            </b-nav>
          </template>
        </b-card>
      </div>
      <b-card-group>
        <b-card class="input-card" style="">
          <!--
            Check
          -->
          <div v-b-modal.modal-prevent-closing>
            <h6>Leaving from</h6>
            <p style="font-weight:bold;">{{ airportCodeOfFrom }}</p>
            <h6>Going To</h6>
            <p style="font-weight:bold;">{{ airportCodeOfTo }}</p>
            <!-- <b-button v-b-modal.modal-prevent-closing variant="success">Options</b-button>-->

            <div class="mt-3"></div>

            <b-modal
              id="modal-prevent-closing"
              ref="modal"
              title="Select City"
              @show="resetModal"
              @hidden="resetModal"
              @ok="handleOk"
            >
              <div>
                <div>
                  <h6>Leaving From</h6>
                  <b-form-input
                    class="input-field"
                    v-model="leavingFrom"
                    placeholder="Dhaka, Bangladesh"
                  ></b-form-input>
                  <div class="mt-2">{{ airportCodeOfFrom }}</div>
                  <div>
                    <h6>Going To</h6>
                    <b-form-input
                      class="input-field"
                      v-model="goingTo"
                      placeholder="Kalkata, India"
                    ></b-form-input>
                    <div class="mt-2">{{ airportCodeOfTo }}</div>
                  </div>
                </div>
              </div>

              <form ref="form" @submit.stop.prevent="handleSubmit"></form>
            </b-modal>
          </div>
          <!--Check end-->
        </b-card>
        <b-card class="input-card">
          <div>
            <h6>Returning On</h6>
            <div>
              <b-form-datepicker
                id="example-datepicker1"
                v-model="returningOn"
                :date-format-options="{
                  month: 'short',
                  year: 'numeric',
                  day: 'numeric'
                }"
                class="mb-2"
              ></b-form-datepicker>
            </div>
            <div class="mt-2" v-if="departuringOn">{{ returningOn }}</div>
          </div>
        </b-card>
        <b-card class="input-card">
          <div>
            <h6>Departuring On</h6>
            <div>
              <b-form-datepicker
                id="example-datepicker"
                v-model="departuringOn"
                :date-format-options="{
                  month: 'short',
                  year: 'numeric',
                  day: 'numeric'
                }"
                class="mb-2"
                style="border:none;"
                placeholder="Select date"
              ></b-form-datepicker>
            </div>
            <div class="mt-2" v-if="departuringOn">{{ departuringOn }}</div>
          </div>
        </b-card>

        <b-card class="input-card">
          <div>
            <h6>Going To</h6>
            <b-form-input
              class="input-field"
              v-model="goingTo"
              placeholder="Kalkata, India"
            ></b-form-input>
            <div class="mt-2">{{ goingTo }}</div>
          </div>
        </b-card>
      </b-card-group>
      <div class="center">
        <button @click="searchFlights()">
          Search
        </button>
      </div>
    </div>
    <!--Test end-->

    <b-nav tabs>
      <b-nav-item active>Available Flight</b-nav-item>
      <b-nav-item v-if="flightData !== undefined" v-on:click="sortUsingPrice"
        >Filter By Price</b-nav-item
      >
      <b-nav-item v-on:click="sortUsingTime">Filter By Time</b-nav-item>
    </b-nav>

    <div class="flight-table">
      <b-container class="bv-example" v-if="morning && evening && flightData">
        <b-row>
          <b-col>
            <b-card class="card-class">
              <p style="text-align:center">{{ morning }} C</p>
            </b-card>
          </b-col>
          <b-col>
            <b-card class="card-class">
              <p style="text-align:center">{{ evening }} C</p>
            </b-card>
          </b-col>
          <b-col>
            <b-card class="card-class">
              <p style="text-align:center">{{ afternoon }} C</p>
            </b-card>
          </b-col>
        </b-row>
      </b-container>

      <li
        style="list-style-type: none;"
        v-for="post of flightData"
        v-if="
          flightData !== undefined &&
            sortByPrice === false &&
            sortByTime === false
        "
      >
        <b-card class="card-class">
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
            sortByPrice === true &&
            sortByTime === false
        "
      >
        <b-card class="card-class">
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
        <b-card class="card-class">
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
    <div></div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Flight",
  data() {
    return {
      /*
      check start
      */
      month: [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec"
      ],
      msg: "Ready for next trip.? Book with us",
      airportCodeOfFrom: "",
      airportCodeOfTo: "",
      goingTo: "DAC",
      leavingFrom: "DXB",
      departuringOn: "2021-12-25",
      returningOn: "2021-12-30",
      adult: 0,
      child: 0,
      name: "",
      nameState: null,
      submittedNames: [],
      /*
      check end
      */
      isOk: 0,
      flightData: [],
      sortByTime: false,
      sortByPrice: false,
      posts: [],
      errors: [],
      morning: "",
      afternoon: "",
      evening: "",
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
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity();
      this.nameState = valid;
      return valid;
    },
    resetModal() {
      this.name = "";
      this.nameState = null;
    },
    handleOk(bvModalEvt) {
      // Prevent modal from closing
      bvModalEvt.preventDefault();
      // Trigger submit handler
      this.handleSubmit();
      this.getAirportCode();
    },
    handleSubmit() {
      // Exit when the form isn't valid
      if (!this.checkFormValidity()) {
        return;
      }
      // Push the name to submitted names
      this.submittedNames.push(this.name);
      // Hide the modal manually
      this.$nextTick(() => {
        this.$bvModal.hide("modal-prevent-closing");
      });
    },
    searchFlights: function() {
      alert("It may take some time. Please wait");
      let flightURL =
        "https://api.sharetrip.net/api/v1/flight/search?tripType=Return&adult=1&child=0&infant=0&class=Economy&origin=" +
        this.airportCodeOfFrom +
        "&destination=" +
        this.airportCodeOfTo +
        "&depart=" +
        this.departuringOn +
        "&depart=" +
        this.returningOn;
      console.log(flightURL);

      axios
        .get(flightURL)
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
                response.data.response.flights[i].flight[0].destinationName
                  .city;
              const originCode =
                response.data.response.flights[i].flight[0].originName.code;
              const destinationAirport =
                response.data.response.flights[i].flight[0].destinationName
                  .airport;
              const destinationCode =
                response.data.response.flights[i].flight[0].destinationName
                  .code;
              const arivalTime =
                response.data.response.flights[i].flight[0].arrivalDateTime
                  .time;
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
      /*
      fetch weather data 
      */
      if (this.goingTo.length > 0) {
        fetch(
          "https://community-open-weather-map.p.rapidapi.com/forecast?q=" +
            this.goingTo,
          {
            method: "GET",
            headers: {
              "x-rapidapi-host": "community-open-weather-map.p.rapidapi.com",
              "x-rapidapi-key":
                "ceff00788dmshc572d2e939e2aa1p16f562jsn6a57c668e74a"
            }
          }
        )
          .then(response => response.json())
          .then(data => {
            console.log(data);
            const morningData = Math.ceil((data.list[0].main.temp + data.list[1].main.temp) / 2 - 273.15 );
            const eveningData = Math.ceil( ((data.list[0].main.temp + data.list[1].main.temp) / 2 - 273.15) *1.8 +32 );
            const afternoonData = Math.ceil(
              (data.list[2].main.temp + data.list[2].main.temp) / 2 - 273.15
            );
            const Data = Math.ceil(
              (data.list[4].main.temp + data.list[5].main.temp) / 2 - 273.15
            );
            this.morning = morningData;
            this.evening = eveningData;
            this.afternoon = afternoonData;
          })
          .catch(err => {
            console.error(err.message);
          });
      }
      /*
     test end
     */
    },
    /*
    Fetching airport code from city name
    */
    getAirportCode: function() {
      let urlString =
        "https://api.sharetrip.net/api/v1/flight/search/airport?name=";
      urlString += this.leavingFrom;
      try {
        axios
          .get(urlString)
          .then(response => {
            response = JSON.stringify(response);
            console.log("Res : " + response);
            response = JSON.parse(response);
            const airportCode = response.data.response[0].iata;
            console.log("Airport code : " + airportCode);
            this.airportCodeOfFrom = airportCode;
          })
          .catch(e => {
            this.errors.push(e);
          });
      } catch (error) {
        console.log(error.message);
      }
      urlString =
        "https://api.sharetrip.net/api/v1/flight/search/airport?name=";
      urlString += this.goingTo;
      try {
        axios
          .get(urlString)
          .then(response => {
            response = JSON.stringify(response);
            console.log("Res : " + response);
            response = JSON.parse(response);
            const destinationAirportCode = response.data.response[0].iata;
            console.log("Airport code : " + destinationAirportCode);
            this.airportCodeOfTo = destinationAirportCode;
          })
          .catch(e => {
            this.errors.push(e);
          });
      } catch (error) {
        console.log(error.message);
      }
    },

    /*
  Method to sort flight by price
  */
    sortUsingPrice: function() {
      this.sortByTime = false;
      this.flightData.sort(function(a, b) {
        return a.price - b.price;
      });
      this.sortByPrice = true;
    },
    /*
    method to sort flight using time 
    */
    sortUsingTime: function() {
      //alert("It works");
      this.sortByPrice = false;
      this.sortByTime = true;
      this.flightData.sort(function(a, b) {
        return a.arivalTime.localeCompare(b.arivalTime);
      });
    }
  }
  
};

/*
test
*/
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Abril+Fatface&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Rubik+Mono+One&display=swap");
/*
styling input field section
*/
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@700&display=swap");

.flight-container {
  text-align: left;
  margin: 0px 0px 0px 0px;
}
.input-container .input-value {
  font-weight: 400;
  color: black;
}
.flight-container .input-card {
  margin: 10px 10px 5px 10px;
  /*font-family: 'Roboto', sans-serif;*/
  /*border: 1px solid black;*/
  border-left: 3px solid#055636;
  border-radius: 10px;
}
.input-field {
  /*border: none;*/
}
.flight-container .center {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
  /*border: 3px solid ; */
}
/*
style search button
*/
.flight-container .center button {
  height: 40px;
  width: 100px;
  border: none;
  color: white;
  background-color: #04aa6d;
  border-radius: 10px;
}
.flight-container .center button:hover {
  height: 40px;
  width: 100px;
  border: 1px solid #04aa6d;
  color: #04aa6d;
  background-color: white;
  border-radius: 10px;
}
@media only screen and (max-width: 1200px) {
  .input-card {
    width: 100%;
  }
}
/*
Starting input field section end
*/

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
.flight-table .card-class {
  margin: 5px 100px 0px 100px;
  border-left: 2px solid pink;
}
@media only screen and (max-width: 1200px) {
  /*Big smartphones [426px -> 600px]*/
  .flight-table .card-class {
    margin: 5px 10px 0px 10px;
    border-left: 2px solid pink;
  }
}
</style>
