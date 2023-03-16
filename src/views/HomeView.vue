<template>
  <div class="q-pa-xl">
    <div class="row justify-center">
      <div class="col-2 text-right q-ma-md">
        <div class="row justify-center">
          <q-avatar square size="120px">
            <img src="/mariotennis.png">
          </q-avatar>
        </div>
        <div class="row justify-center avatar-text">
          Player 1
        </div>
        <div class="row justify-center text-h4">
          {{ scores[0] }}
        </div>
        <div class="row justify-center">
          <q-btn color="positive" icon="add_circle" label="Score" @click="addScore(0)" v-if="!finished"  />
        </div>
      </div>
      <div class="col-6 text-center q-ma-md items-center">
        <div class="row justify-center">
          <q-card class="bg-secondary text-white q-pa-md text-h2">
            <q-card-section>
              {{ scoreText }}
            </q-card-section>
          </q-card>
        </div>
        <div class="row justify-center q-ma-md">
          <q-btn color="negative" icon="autorenew" label="Reset" @click="resetScore()" />
        </div>
      </div>
      <div class="col-2 text-right q-ma-md">
        <div class="row justify-center">
          <q-avatar square size="120px">
            <img src="/Luigi.png">
          </q-avatar>
        </div>
        <div class="row justify-center avatar-text">
          Player 2
        </div>
        <div class="row justify-center text-h4">
          {{ scores[1] }}
        </div>
        <div class="row justify-center">
          <q-btn color="positive" icon="add_circle" label="Score" @click="addScore(1)" v-if="!finished"  />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const players = ref(['player1', 'player2'])
const finished = ref(false)
const scores = ref([0,0])
const scoreText = ref('Love - Love')
const scoreArr = [
  'Love',
  'Fifteen',
  'Thirty',
  'Forty'
]

const addScore = (index) => {
  const op = index == 0 ? 1 : 0
  scores.value[index]++
  console.log(scores.value)
  if (scores.value[index] >= 4 && scores.value[index] - scores.value[op] >= 2) {
    scoreText.value = 'Won for ' + players.value[index]
    finished.value = true
  } else if (scores.value[0] == scores.value[1] && scores.value[0] >= 3) {
    scoreText.value = 'Deuce'
  } else if (scores.value[0] >= 3 && scores.value[1] >= 3 && (scores.value[0] - scores.value[1] == 1 || scores.value[1] - scores.value[0] == 1)) {
    if (scores.value[0] > scores.value[1]) {
      scoreText.value = 'Advantage for player1'
    } else {
      scoreText.value = 'Advantage for player2'
    }
  } else {
    scoreText.value = scoreArr[scores.value[0]] + ' - ' + scoreArr[scores.value[1]]
  }
}

const resetScore = () => {
  finished.value = false
  scores.value = [0,0]
  scoreText.value = 'Love - Love'
}
</script>

<style scoped>
.avatar-text {
  font-size: 22px;
}
</style>