<template>
  <div class="d-flex flex-row justify-content-between mb-2">

    <div class="mr-2 airline-logo align-self-center">
      <img :src="`https://puntcdn.com/code-tests/full-stack/${leg.airline_id}.png`" :alt="leg.airline_name" />
    </div>

    <div class="p-1">
      <p class="card-title">{{ leg.departure_time | moment("HH:mm") }}</p>
      <p class="card-subtitle text-muted">{{ leg.departure_airport }}</p>
    </div>

    <div class="p-1 align-self-center text-muted">
      <ArrowRight />
    </div>

    <div class="p-1">
      <p class="card-title">{{ leg.arrival_time | moment("HH:mm") }}</p>
      <p class="card-subtitle text-muted">{{ leg.arrival_airport }}</p>
    </div>

    <div class="p-1 ml-auto duration align-self-center">
      <p class="text-muted mb-1">{{ duration }}</p>
      <p class="text-main mb-0">Direct</p>
    </div>
  </div>
</template>

<script>
import ArrowRight from 'vue-material-design-icons/ArrowRight'
import moment from 'moment'

export default {
  name: 'Leg',
  components: {
    ArrowRight
  },
  props: {
    leg: Object,
  },
  computed: {
    duration() {
      return moment.utc().startOf('day').add({ minutes: this.leg.duration_mins }).format('H[h] mm[m]')
    }
  }
}
</script>

<style scoped>
.airline-logo {
  vertical-align: middle;
}
.airline-logo img {
  width: 40px;
  height: 40px;
}
.text-main {
  color: #25a698;
}
.duration {
  font-size: 0.90rem
}
</style>
