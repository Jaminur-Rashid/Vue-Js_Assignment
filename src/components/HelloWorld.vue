<template>
  <div class="card-container">
  <!--<div style="height:30px;width:100%;font-weight:700;background-color: #d9d9d9"> {{msg}}</div>-->
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
        <b-card class="input-card">
          <!--
            Check
          -->
          <div>
            <h6>Guest</h6>
            <b-button v-b-modal.modal-prevent-closing>Options</b-button>

            <div class="mt-3"></div>

            <b-modal
              id="modal-prevent-closing"
              ref="modal"
              title="Select Cabin class and Number of passenger"
              @show="resetModal"
              @hidden="resetModal"
              @ok="handleOk"
            >
              <div>
                <p>Adult : {{ adult }}</p>
                <button @click="addOne">+</button>
                <button @click="minusOne">-</button>
                <span>Adult</span>
              </div>

              <form ref="form" @submit.stop.prevent="handleSubmit">
                <!--
        <b-form-group
          label="Name"
          label-for="name-input"
          invalid-feedback="Name is required"
          :state="nameState"
        >
          <b-form-input
            id="name-input"
            v-model="name"
            :state="nameState"
            required
          ></b-form-input>
        </b-form-group>
        -->
              </form>
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
                class="mb-2"
              ></b-form-datepicker>
            </div>
          </div>
        </b-card>
        <b-card class="input-card">
          <div>
            <h6>Departuring On</h6>
            <div>
              <b-form-datepicker
                id="example-datepicker"
                v-model="departuringOn"
                :date-format-options="{  month: 'short',year: 'numeric', day: 'numeric' }"
                class="mb-2"
                style="border:none"
              ></b-form-datepicker>
            </div>
            <div class="mt-2" v-if="departuringOn">{{departuringOn}}</div>
          </div>
        </b-card>

        <b-card class="input-card">
          <div>
            <h6>Leaving From </h6>
            <b-form-input
              class="input-field"
              v-model="leavingFrom"
              placeholder="Dhaka, Bangladesh"
            ></b-form-input>
            <div class="mt-2">{{ leavingFrom }}</div>
          </div>
        </b-card>
        <b-card  class="input-card">
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
        <button>
          Search
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      month : ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul","Aug", "Sep", "Oct", "Nov", "Dec"],
      msg: "Ready for next trip.? Book with us",
      goingTo: "Dhaka, Bangladesh",
      leavingFrom: "",
      departuringOn: "",
      returningOn: "",
      adult: 0,
      child: 0,
      name: "",
      nameState: null,
      submittedNames: []
    };
  },
  methods: {
    /*
     Methods to increase passenger
     */
    addOne: function() {
      let totPass = this.adult;
      if (totPass <= 10) {
        this.adult = totPass + 1;
      }
    },
    /*
     Methods to decrese passenger
     */
    minusOne: function() {
      let totPass = this.adult;
      if (totPass > 0) {
        this.adult = totPass - 1;
      }
    },
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
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@700&display=swap");

.card-container {
  text-align: left;
  margin: 0px 0px 0px 0px;
}
.input-container .input-value {
  font-weight: 400;
  color: black;
}
.card-container .input-card {
  margin: 10px 10px 5px 10px;
  /*font-family: 'Roboto', sans-serif;*/
  /*border: 1px solid black;*/
  border-left: 3px solid teal;
}
.input-field {
  border: none;
}
.card-container .center {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
  /*border: 3px solid ; */
}
.card-container .center button {
  background-color: turquoise;
  height: 40px;
  width: 100px;
  border: none;
  color: white;
}
@media only screen and (max-width: 1200px) {
  .input-card {
    width: 100%;
  }
}
</style>
<!--
          <b-card-text>
            This is a wider card with supporting text below as a natural lead-in
            to additional content. This content is a little bit longer.
          </b-card-text>
          <template #footer>
            <div class="input-container">
              <b-form-input
                v-model="departuringOn"
                placeholder="Enter your name"
              ></b-form-input>
              <div class="mt-2 input-value" >{{ departuringOn }}</div>
            </div>
          </template>
          -->
