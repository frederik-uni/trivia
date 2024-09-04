<template>
  <div>
    <h2>Select Timer</h2>
    <select v-model="selectedTime">
      <option value="5">5 seconds</option>
      <option value="10">10 seconds</option>
      <option value="15">15 seconds</option>
      <option value="30">30 seconds</option>
      <option value="40">40 seconds</option>
      <option value="50">50 seconds</option>
      <option value="60">60 seconds</option>
      <option value="70">1 minute 10 seconds</option>
      <option value="80">1 minute 20 seconds</option>
      <option value="90">1 minute 30 seconds</option>
      <option value="100">1 minute 40 seconds</option>
      <option value="110">1 minute 50 seconds</option>
      <option value="120">2 minutes</option>
      <option value="130">2 minute 10 seconds</option>
      <option value="140">2 minute 20 seconds</option>
      <option value="150">2 minute 30 seconds</option>
      <option value="160">2 minute 40 seconds</option>
      <option value="170">2 minute 50 seconds</option>
      <option value="180">3 minutes</option>
      <option value="190">3 minute 10 seconds</option>
      <option value="200">3 minute 20 seconds</option>
      <option value="210">3 minute 30 seconds</option>
      <option value="220">3 minute 40 seconds</option>
      <option value="230">3 minute 50 seconds</option>
      <option value="240">4 minutes</option>
      <option value="300">5 minutes</option>
      <option value="360">6 minutes</option>
      <option value="420">7 minutes</option>
      <option value="480">8 minutes</option>
      <option value="540">9 minutes</option>
      <option value="600">10 minutes</option>
      <option value="660">11 minutes</option>
      <option value="720">12 minutes</option>
      <option value="780">13 minutes</option>
      <option value="840">14 minutes</option>
      <option value="900">15 minutes</option>
      <option value="960">16 minutes</option>
      <option value="1020">17 minutes</option>
      <option value="1080">18 minutes</option>
      <option value="1140">19 minutes</option>
      <option value="1200">20 minutes</option>
      <option value="1260">21 minutes</option>
      <option value="1320">22 minutes</option>
      <option value="1380">23 minutes</option>
      <option value="1440">24 minutes</option>
      <option value="1500">25 minutes</option>
      <option value="1560">26 minutes</option>
      <option value="1620">27 minutes</option>
      <option value="1680">28 minutes</option>
      <option value="1740">29 minutes</option>
      <option value="1800">30 minutes</option>
    </select>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      selectedTime: 60
    }
  },
  methods: {
    getSelectedTime() {
      return this.selectedTime
    }
  }
}
</script>
