<template>
  <div class="img-container">
    <h1 class="center">Ready for next trip.? Book with us.</h1>
    
    <img
      style="height:350px;width:100%"
      src="https://i.ibb.co/HK6VHMz/Flight.jpg"
    />
  </div>
</template>

<script>
export default {
  name: "SlideShow",
  data() {
    return {
      m: ""
    };
  },
  methods: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@700&display=swap");
@import url('https://fonts.googleapis.com/css2?family=Abril+Fatface&display=swap');
.img-container {
  position: relative;
  text-align: center;
  color:#ffffff;
}
.center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-family: 'Abril Fatface', cursive;
}
.center-one {
  position: absolute;
  top: 60%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-family: 'Roboto';
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
