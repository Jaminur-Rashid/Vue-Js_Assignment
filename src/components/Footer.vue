<template>
    <div class="footer-div">
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

export default {
  name: "Footer",
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

.footer-div{
    margin:500px 30px 0px 30px;
    position: relative;
}
 .f-card{
    background-color: #055636;
    color:#ffffff;
    border-right: 1px solid #ffffff;
}

</style>