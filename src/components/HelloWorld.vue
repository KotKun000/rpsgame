<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)

</script>

<template>
  <div>
    <h1>เกมเป่ายิ้งฉุบ</h1>
    <div>
      <h2>ฝ่ายแดง: {{ redScore }}</h2>
      <h2>ฝ่ายน้ำเงิน: {{ blueScore }}</h2>
    </div>
    <div>
      <button @click="startGame">เริ่มเกม</button>
      <button @click="resetGame">รีเซ็ตคะแนน</button>
    </div>
    <div>
      <h2>ผลลัพธ์: {{ result }}</h2>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      redScore: 0,
      blueScore: 0,
      result: "",
      choices: ["rock", "paper", "scissors", "love"],
    };
  },
  methods: {
    startGame() {
      this.redScore = 0;
      this.blueScore = 0;
      this.result = "";
      this.playRound();
    },
    resetGame() {
      this.redScore = 0;
      this.blueScore = 0;
      this.result = "";
    },
    playRound() {
      const redChoice = this.choices[Math.floor(Math.random() * 4)];
      const blueChoice = this.choices[Math.floor(Math.random() * 4)];

      if (redChoice === blueChoice) {
        this.result = "เสมอ";
      } else if (
        (redChoice === "rock" && blueChoice === "scissors") ||
        (redChoice === "scissors" && blueChoice === "paper") ||
        (redChoice === "paper" && blueChoice === "rock") ||
        (redChoice === "love" && blueChoice !== "love")
      ) {
        this.redScore++;
        this.result = "ฝ่ายแดงชนะ";
      } else {
        this.blueScore++;
        this.result = "ฝ่ายน้ำเงินชนะ";
      }
    },
  },
  mounted() {
    this.startGame();
  },
};
</script>

<style scoped>
/* สไตล์ CSS ตามที่คุณต้องการ */
</style>



<style scoped>
.read-the-docs {
  color: #888;
}
</style>
