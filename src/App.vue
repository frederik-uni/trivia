<template>
  <div id="app">
    <div v-if="!did_start">
      <TimerOptions ref="timerOptions" />
      <UploadAndStart @start-timer="startQuiz" />
    </div>
    <div v-if="currentQuestion" class="question-container">
      <div v-if="!isPromptingForAnswer" class="question-content">
        <div v-if="peekQuestion" class="peek-question">
          <h2 v-if="peekQuestion.text && peekQuestion.img_background" class="absolute">
            {{ peekQuestion.text }}
          </h2>
          <h2 v-if="peekQuestion.text && !peekQuestion.img_background" class="question-text">
            {{ peekQuestion.text }}
          </h2>
          <div class="image-container">
            <img
              v-if="peekQuestion.img"
              :src="peekQuestion.img"
              alt="Question Image"
              class="question-image"
            />
          </div>
        </div>
        <h3 class="countdown">{{ countdown }}</h3>
      </div>

      <div v-else>
        <h3
          v-if="
            currentQuestion.possible_solutions &&
            currentQuestion.possible_solutions.length > 0 &&
            !answerSubmitted
          "
        >
          Time's up! What's your answer?
        </h3>
        <div
          v-if="
            currentQuestion.possible_solutions &&
            currentQuestion.possible_solutions.length > 0 &&
            !answerSubmitted
          "
        >
          <button
            v-for="(solution, index) in currentQuestion.possible_solutions"
            class="solution-buttons"
            :key="index"
            @click="submitAnswer(index)"
          >
            {{ solution }}
          </button>
        </div>

        <div v-if="answerSubmitted">
          <h4>{{ answerMessage }}</h4>
          <button @click="nextQuestion" class="next-button">Next</button>
        </div>

        <div
          v-else-if="
            !currentQuestion.possible_solutions || currentQuestion.possible_solutions.length === 0
          "
        >
          <button @click="nextQuestion" class="next-button">Next</button>
        </div>
      </div>
    </div>

    <div v-if="jsonData && !isPromptingForAnswer">
      <div class="overlay left-overlay" @click="peekPrevious"></div>
      <div class="overlay right-overlay" @click="peekNext"></div>
    </div>
  </div>
</template>

<style>
html,
body {
  margin: 0;
  padding: 0;
  overflow: hidden;
  height: 100%;
}
</style>
<style scoped>
html,
body {
  margin: 0;
  padding: 0;
  overflow: hidden;
  height: 100%;
}

#app {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.question-container {
  text-align: center;
  position: relative;
  width: 100%;
  height: 100%;
}

.peek-question {
  text-align: center;
  margin-bottom: 20px;
}

.question-text {
  margin: 0;
  font-size: 1.5em;
  word-wrap: break-word;
  padding: 1em;
  box-sizing: border-box;
}

.image-container {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}
.image-container img {
  max-width: 100%;
  max-height: 100%;
  width: auto;
  height: auto;
}

.countdown {
  position: absolute;
  bottom: 20px;
  right: 20px;
  font-size: 2em;
  color: red;
}
.overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  width: 50%;
  cursor: pointer;
  z-index: 999;
}

.left-overlay {
  left: 0;
  background-color: rgba(0, 0, 0, 0);
}

.right-overlay {
  right: 0;
  background-color: rgba(0, 0, 0, 0);
}

.solution-buttons {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.solution-buttons button {
  margin: 5px;
}
.absolute {
  position: absolute;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  text-align: center;
  width: 100%;
  margin: 0;
  padding: 0;
  text-shadow:
    1px 1px 0 #fff,
    -1px -1px 0 #fff,
    1px -1px 0 #fff,
    -1px 1px 0 #fff;
}

button {
  margin: 5px;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 1em;
  cursor: pointer;
}

.next-button {
  background-color: blue;
  color: white;
  font-size: 1.5em;
  padding: 15px 30px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>

<script>
import TimerOptions from './components/TimerOptions.vue'
import UploadAndStart from './components/UploadAndStart.vue'

export default {
  components: {
    TimerOptions,
    UploadAndStart
  },
  data() {
    return {
      jsonData: null,
      currentQuestionIndex: 0,
      peekIndex: 0,
      countdown: 0,
      timerInterval: null,
      isPromptingForAnswer: false,
      answerSubmitted: false,
      answerMessage: '',
      answeredQuestions: new Set()
    }
  },
  computed: {
    currentQuestion() {
      return this.jsonData ? this.jsonData[this.currentQuestionIndex] : null
    },
    peekQuestion() {
      return this.jsonData ? this.jsonData[this.peekIndex] : null
    }
  },
  methods: {
    startQuiz(jsonData) {
      this.jsonData = jsonData
      this.answeredQuestions.clear()
      this.peekIndex = 0
      this.countdown_time = this.$refs.timerOptions.getSelectedTime()
      this.did_start = true
      this.startNextQuestion()
    },
    startNextQuestion() {
      this.isPromptingForAnswer = false
      this.answerSubmitted = false
      this.answerMessage = ''
      this.countdown = this.countdown_time

      if (this.timerInterval) {
        clearInterval(this.timerInterval)
      }

      this.timerInterval = setInterval(() => {
        if (this.countdown > 0) {
          this.countdown--
        } else {
          clearInterval(this.timerInterval)
          this.isPromptingForAnswer = true
        }
      }, 1000)
    },
    submitAnswer(selectedIndex) {
      this.answerSubmitted = true
      const correctAnswerIndex = this.currentQuestion.correct_solutions
      if (selectedIndex === correctAnswerIndex) {
        this.answerMessage = 'Correct!'
      } else {
        this.answerMessage = 'Wrong answer.'
      }
    },
    nextQuestion() {
      this.answeredQuestions.add(this.currentQuestionIndex)
      this.currentQuestionIndex++
      if (this.currentQuestionIndex < this.jsonData.length) {
        this.peekIndex = this.currentQuestionIndex
        this.startNextQuestion()
      } else {
        this.did_start = false
        alert('Quiz completed!')
        this.resetQuiz()
      }
    },
    peekPrevious() {
      if (this.peekIndex > 0 && !this.answeredQuestions.has(this.peekIndex - 1)) {
        this.peekIndex--
      }
    },
    peekNext() {
      if (
        this.peekIndex < this.jsonData.length - 1 &&
        !this.answeredQuestions.has(this.peekIndex + 1)
      ) {
        this.peekIndex++
      }
    },
    resetQuiz() {
      this.currentQuestionIndex = 0
      this.peekIndex = 0
      this.jsonData = null
      this.countdown = 0
      this.isPromptingForAnswer = false
      this.answerSubmitted = false
      this.answeredQuestions.clear()
    }
  }
}
</script>
