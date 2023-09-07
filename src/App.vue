<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <h1>เกมเป่ายิ้งฉุบ</h1>
    <div class="players">
      <div class="player">
        <h2>ฝ่ายแดง</h2>
        <img :src="redChoiceImage" alt="ฝ่ายแดง" />
        <p>{{ redChoice }}</p>
      </div>
      <div class="player">
        <h2>ฝ่ายน้ำเงิน</h2>
        <img :src="blueChoiceImage" alt="ฝ่ายน้ำเงิน" />
        <p>{{ blueChoice }}</p>
      </div>
    </div>
    <div>
      <h2>ผลลัพธ์: {{ result }}</h2>
    </div>
    <div class="RB">
      <h2>คะแนน</h2>
      <p>ฝ่ายแดง: {{ redScore }}</p>
      <p>ฝ่ายน้ำเงิน: {{ blueScore }}</p>
    </div>
    <div>
      <button @click="playRound">เล่นเกม</button>
      <button @click="resetGame">รีเซ็ตคะแนน</button>
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
      choices: ["hammer", "scissors", "paper", "love"],
      redChoice: "",
      blueChoice: "",
      redChoiceImage: "",
      blueChoiceImage: "",
      images: {
        hammer: "https://cdn-icons-png.flaticon.com/512/6121/6121152.png",
        scissors: "https://cdn-icons-png.flaticon.com/512/5418/5418004.png",
        paper: "https://png.pngtree.com/png-vector/20221010/ourmid/pngtree-paper-icon-png-image_6294297.png",
        love: "https://media.tenor.com/QB0-30vY4s4AAAAi/hu-tao-love.gif",
      },
    };
  },
  methods: {
    playRound() {
      this.redChoice = this.choices[Math.floor(Math.random() * 4)];
      this.blueChoice = this.choices[Math.floor(Math.random() * 4)];

      this.redChoiceImage = this.images[this.redChoice];
      this.blueChoiceImage = this.images[this.blueChoice];

      if (this.redChoice === this.blueChoice) {
        this.result = "เสมอ";
      } else if (this.redChoice === "love" || this.blueChoice === "love") {
        this.result = "ความรักชนะทุกสิ่ง";
        this.redScore++;
      } else {
        this.result = this.getWinner(this.redChoice, this.blueChoice);
        if (this.result === "ฝ่ายแดงชนะ") {
          this.redScore++;
        } else {
          this.blueScore++;
        }
      }
    },
    resetGame() {
      this.redScore = 0;
      this.blueScore = 0;
      this.result = "";
      this.redChoice = "";
      this.blueChoice = "";
      this.redChoiceImage = "";
      this.blueChoiceImage = "";
    },
    getWinner(red, blue) {
      if (
        (red === "hammer" && blue === "scissors") ||
        (red === "scissors" && blue === "paper") ||
        (red === "paper" && blue === "hammer")
      ) {
        return "ฝ่ายแดงชนะ";
      } else {
        return "ฝ่ายน้ำเงินชนะ";
      }
    },
  },
};
</script>

<style scoped>
.players {
  display: flex;
  justify-content: space-around;
}

.player {
  text-align: center;
  font-size: 1.2rem;
  font-weight: bolder;
  
  
}

.player img {
  max-width: 120px;
  max-height: 120px;
  background-size: cover;
  
}

button {
  font-size: 18px;
  margin: 10px;
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #4fa1f8;
}
.RB{
  font-weight: bolder;
  font-size: 1.5rem;
}



</style>







