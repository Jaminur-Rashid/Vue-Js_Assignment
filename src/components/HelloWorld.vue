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
        <b-card class="input-card" style="">
          <!--
            Check
          -->
          <div v-b-modal.modal-prevent-closing>
            <h6>Leaving from</h6>
            <p style="font-weight:bold;">{{leavingFrom}}</p>
            <h6>Going To</h6>
            <p style="font-weight:bold;">{{goingTo}}</p>
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
            <h6>Leaving From </h6>
            <b-form-input
              class="input-field"
              v-model="leavingFrom"
              placeholder="Dhaka, Bangladesh"
            ></b-form-input>
            <div class="mt-2">{{ leavingFrom }}</div>
            <div>
            <h6>Going To</h6>
            <b-form-input
              class="input-field"
              v-model="goingTo"
              placeholder="Kalkata, India"
            ></b-form-input>
            <div class="mt-2">{{ goingTo }}</div>
          </div>
          </div>
              </div>

              <form ref="form" @submit.stop.prevent="handleSubmit">
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
                style="border:none;"
                placeholder="Select date"
              ></b-form-datepicker>
            </div>
            <div class="mt-2" v-if="departuringOn">{{departuringOn}}</div>
          </div>
        </b-card>
<!--
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
        -->
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
      leavingFrom: "khulna",
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
  border-left: 3px solid#055636;
  border-radius: 10px;
}
.input-field {
  /*border: none;*/
}
.card-container .center {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
  /*border: 3px solid ; */
}
/*
style search button
*/
.card-container .center button {
  height: 40px;
  width: 100px;
  border: none;
  color: white;
  background-color: #04AA6D;
  border-radius: 10px;
}
.card-container .center button:hover {
  height: 40px;
  width: 100px;
  border: 1px solid #04AA6D;
  color: #04AA6D;
  background-color:white;
  border-radius: 10px;
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
