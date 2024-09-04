<template>
  <div>
    <h2>Upload JSON File</h2>
    <input type="file" @change="onFileChange" accept=".json" />
    <button @click="startQuiz">Start</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      jsonData: null
    }
  },
  methods: {
    onFileChange(event) {
      const file = event.target.files[0]

      if (!file) {
        alert('Please select a file.')
        return
      }

      if (file.type !== 'application/json') {
        alert('Please select a JSON file.')
        return
      }

      const reader = new FileReader()

      reader.onload = (e) => {
        try {
          this.jsonData = JSON.parse(e.target.result)
          console.log('Parsed JSON:', this.jsonData)
        } catch (error) {
          alert('There was an error parsing the JSON file.')
        }
      }

      reader.readAsText(file)
    },
    startQuiz() {
      if (this.jsonData) {
        this.$emit('start-timer', this.jsonData)
      } else {
        alert('Please upload a JSON file first.')
      }
    }
  }
}
</script>
