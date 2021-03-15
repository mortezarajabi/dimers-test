<template>
  <div class="col-md-4" >
    <div class="card mb-4 box-shadow">
      <div class="card-body p-2">

        <Leg v-for="(leg, index) in legs" :key="index" :leg="leg" />

        <div class="d-flex flex-row justify-content-between mb-0 mt-3 align-self-end">
          <div class="p-1">
            <p class="price mb-0 font-weight-bold">{{ flight.price }}</p>
            <p class="website text-muted mb-0">{{ flight.agent }}</p>
          </div>
          <div class="p-1">
              <a href="#" class="btn btn-main my-2 font-weight-bold">Select</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Leg from './Leg'

export default {
  name: 'Flight',
  components: {
    Leg
  },
  props: {
    flight: Object,
    getLeg: Function
  },
  data() {
    return {
      legs: []
    }
  },
  created() {

    this.setLegs()
  },
  methods: {
    setLegs() {
       this.flight?.legs.forEach(legId => {
         let leg = this.getLeg(legId)
         this.legs.push(leg);
       })
    }
  }
}
</script>


<style scoped>

.price {
  font-size: 1.5rem;
  line-height: 1;
}
.btn-main {
  background-color: #25a698;
  color: #fff
}
</style>
