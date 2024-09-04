<template>
  <div>
    <h2>Select Timer</h2>
    <select v-model="selectedTime">
      <option value="5000">5 seconds</option>
      <option value="10000">10 seconds</option>
      <option value="15000">15 seconds</option>
      <option value="30000">30 seconds</option>
      <option value="40000">40 seconds</option>
      <option value="50000">50 seconds</option>
      <option value="60000">60 seconds</option>
      <option value="70000">1 minute 10 seconds</option>
      <option value="80000">1 minute 20 seconds</option>
      <option value="90000">1 minute 30 seconds</option>
      <option value="100000">1 minute 40 seconds</option>
      <option value="110000">1 minute 50 seconds</option>
      <option value="120000">2 minutes</option>
      <option value="130000">2 minute 10 seconds</option>
      <option value="140000">2 minute 20 seconds</option>
      <option value="150000">2 minute 30 seconds</option>
      <option value="160000">2 minute 40 seconds</option>
      <option value="170000">2 minute 50 seconds</option>
      <option value="180000">3 minutes</option>
      <option value="190000">3 minute 10 seconds</option>
      <option value="200000">3 minute 20 seconds</option>
      <option value="210000">3 minute 30 seconds</option>
      <option value="220000">3 minute 40 seconds</option>
      <option value="230000">3 minute 50 seconds</option>
      <option value="240000">4 minutes</option>
      <option value="300000">5 minutes</option>
      <option value="360000">6 minutes</option>
      <option value="420000">7 minutes</option>
      <option value="480000">8 minutes</option>
      <option value="540000">9 minutes</option>
      <option value="600000">10 minutes</option>
      <option value="660000">11 minutes</option>
      <option value="720000">12 minutes</option>
      <option value="780000">13 minutes</option>
      <option value="840000">14 minutes</option>
      <option value="900000">15 minutes</option>
      <option value="960000">16 minutes</option>
      <option value="1020000">17 minutes</option>
      <option value="1080000">18 minutes</option>
      <option value="1140000">19 minutes</option>
      <option value="1200000">20 minutes</option>
      <option value="1260000">21 minutes</option>
      <option value="1320000">22 minutes</option>
      <option value="1380000">23 minutes</option>
      <option value="1440000">24 minutes</option>
      <option value="1500000">25 minutes</option>
      <option value="1560000">26 minutes</option>
      <option value="1620000">27 minutes</option>
      <option value="1680000">28 minutes</option>
      <option value="1740000">29 minutes</option>
      <option value="1800000">30 minutes</option>
    </select>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      selectedTime: 60000
    }
  },
  methods: {
    getSelectedTime() {
      return this.selectedTime
    }
  }
}
</script>
