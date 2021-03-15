<template>
  <div>
    <section class="jumbotron mt-5 mb-0" style="background-image:url(//content.skyscnr.com/m/785bdfcbe683606c/Large-Flights-hero-2.jpg?crop=1800px:1375px&quality=60)">
      <div class="container">
        <h1 class="jumbotron-heading">Let the journey begin</h1>
      </div>
    </section>
    <div class="py-5 bg-light">
      <div class="container">

        <div class="row" v-if="flights.length">
          <Flight v-for="flight in flights" :key="flight.id" :flight="flight" :getLeg="getLeg" />
        </div>

        <div class="row" v-if="loading">
          <div class="col text-center">
            <p>Loading...</p>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import Flight from './components/Flight.vue';
import Axios from 'axios';

export default {
  name: 'App',
  components: {
    Flight
  },
  created () {
    this.fetchData()
  },
  data () {
    return {
      loading: false,
      flights: null,
      error: null,
      legs: null
    }
  },
  methods: {
    fetchData () {
      this.error = this.flights = null
      this.loading = true

      Axios.get("/data/flights.json")
          .then(result => {
            this.flights = result.data.itineraries
            this.legs = result.data.legs
            this.loading = false
          })
        .catch(error => {
          console.log(error)
          this.loading = false
          this.error = true;
        })
    },
    getLeg(legId) {
      return this.legs.find(leg =>  leg.id == legId)
    }
  }
}
</script>

<style>
.jumbotron {
  background-repeat: no-repeat;
  background-position: 50% 60%;
  background-size: cover;
  color: #fff;
}
.jumbotron .container {
  min-height: 250px;
}
</style>
