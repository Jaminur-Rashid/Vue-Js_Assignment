<template>
  <div id="app">
    <div class="top-navbar">
  <b-navbar toggleable="lg">
    <b-navbar-brand href="#" id="logo">FlightForAll.com</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item href="#" class="nav-link" style="color:blue">Offer</b-nav-item>
        <b-nav-item href="#" class="nav-link">Manage</b-nav-item>
        <b-nav-item href="#" class="nav-link">Experience</b-nav-item>
        <b-nav-item href="#" class="nav-link">Marco Polo Club</b-nav-item>
        <b-nav-item href="#" class="nav-link">Business</b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="aa" style="float:right">

        <b-nav-item-dropdown right>
          <!-- Using 'button-content' slot -->
          <template #button-content>
            <em>User</em>
          </template>
          <b-dropdown-item href="#">Profile</b-dropdown-item>
          <b-dropdown-item href="#">Sign Out</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>
<SlideShow/>
<AvailableFlight />
<Footer/>
  </div>
  
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Navbar from './components/Heading'
import SlideShow from './components/SlideShow.vue'
import Footer from './components/Footer.vue'
import AvailableFlight from './components/AvailableFlight.vue'

export default {
  name: 'App',
  components: {
    SlideShow,
    Footer,
    AvailableFlight
  }
}
</script>

<style>
#app {
 /* font-family: 'Avenir', Helvetica, Arial, sans-serif;*/
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}
.top-navbar{
  background-color:#ffffff;
}
.top-navbar #logo{
  margin-left: 7px;
  font-family: 'Times New Roman', Times, serif;
  color:red;
  font-weight: 900;
}
.top-navbar .nav-link{
  margin-left: 10px;
  color:purple;
  float:right;

}
.top-navbar{
  background-color:white;
  color: #ffffff;
  color:black;
  margin-bottom: 3px;
}
</style>
