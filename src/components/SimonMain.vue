<template>
  <div>
    <CirclePart
      v-for="(style, index) in styles"
      :key="index"
      :style="style"
      :id="index + 1"
      :pickingColor="pickingColor"
    />
    <Center
      :counter="counter"
      :powerCheckBox="powerCheckBox"
      :startButtonClick="startButtonClick"
    />
    <div class="difficult">
      Уровень сложности
      <ul>
        <li><button @click="setDifficult" id="easy">Легкий</button></li>
        <li><button @click="setDifficult" id="medium">Средний</button></li>
        <li><button @click="setDifficult" id="hard">Тяжелый</button></li>
      </ul>
    </div>
  </div>
</template>

<script>
import CirclePart from "./CirclePart";
import Center from "./Center";

export default {
  components: {
    Center,
    CirclePart,
  },
  methods: {
    setDifficult() {
      switch (event.target.id) {
        case "easy":
          this.reset();
          this.$data.counter = "--";
          this.clearColor();
          this.$data.difficult = 1500;
          break;
        case "medium":
          this.reset();
          this.$data.counter = "--";
          this.clearColor();
          this.$data.difficult = 1000;
          break;
        case "hard":
          this.reset();
          this.$data.counter = "--";
          this.clearColor();
          this.$data.difficult = 400;
          break;
      }
    },
    reset() {
      this.$data.playerOrder = [];
      this.$data.compTurn = true;
      this.$data.flash = 0;
      this.$data.counter = this.$data.turn;
    },
    powerCheckBox() {
      if (event.target.checked) {
        this.$data.power = true;
        this.$data.counter = "--";
      } else {
        this.$data.power = false;
        this.$data.counter = "";
        this.clearColor();
        clearInterval(this.$data.intervalId);
      }
    },
    startButtonClick() {
      if (this.$data.power || this.$data.win) this.play();
    },
    play() {
      (this.$data.win = false),
        (this.$data.order = []),
        (this.$data.playerOrder = []),
        (this.$data.flash = 0),
        (this.$data.intervalId = 0),
        (this.$data.turn = 1);
      this.$data.counter = 1;
      this.$data.good = true;
      for (let i = 0; i < 5; i++) {
        this.$data.order.push(Math.floor(Math.random() * 4) + 1);
      }
      this.$data.compTurn = true;
      this.$data.intervalId = setInterval(this.gameTurn, 800);
    },
    gameTurn() {
      this.$data.power = false;
      if (this.$data.flash == this.$data.turn) {
        clearInterval(this.$data.intervalId);
        this.$data.compTurn = false;
        this.clearColor();
        this.$data.power = true;
      }
      if (this.$data.compTurn) {
        this.clearColor();
        setTimeout(() => {
          if (this.$data.order[this.$data.flash] == 1) this.one();
          if (this.$data.order[this.$data.flash] == 2) this.two();
          if (this.$data.order[this.$data.flash] == 3) this.three();
          if (this.$data.order[this.$data.flash] == 4) this.four();
          this.$data.flash++;
        }, 200);
      }
    },
    one() {
      if (this.$data.noise) {
        let audio = document.getElementById("clip1");
        audio.play();
      }
      this.$data.noise = true;
      this.$data.styles[0].background = "lightgreen";
    },
    two() {
      if (this.$data.noise) {
        let audio2 = document.getElementById("clip2");
        audio2.play();
      }
      this.$data.noise = true;
      this.$data.styles[1].background = "tomato";
    },
    three() {
      if (this.$data.noise) {
        let audio3 = document.getElementById("clip3");
        audio3.play();
      }
      this.$data.noise = true;
      this.$data.styles[2].background = "yellow";
    },
    four() {
      if (this.$data.noise) {
        let audio4 = document.getElementById("clip4");
        audio4.play();
      }
      this.$data.noise = true;
      this.$data.styles[3].background = "lightskyblue";
    },
    clearColor() {
      this.$data.styles[0].background = "darkgreen";
      this.$data.styles[1].background = "darkred";
      this.$data.styles[2].background = "goldenrod";
      this.$data.styles[3].background = "darkblue";
    },
    pickingColor() {
      if (this.$data.power) {
        this.$data.playerOrder.push(+event.target.id);
        this.check();
        switch (+event.target.id) {
          case 1:
            this.one();
            break;
          case 2:
            this.two();
            break;
          case 3:
            this.three();
            break;
          case 4:
            this.four();
            break;
        }
        if (!this.$data.win) {
          setTimeout(() => {
            this.clearColor();
          }, 400);
        }
      }
    },
    check() {
      if (
        this.$data.playerOrder[this.$data.playerOrder.length - 1] !==
        this.$data.order[this.$data.playerOrder.length - 1]
      ) {
        this.$data.good = false;
      }
      if (this.$data.playerOrder.length == 5 && this.$data.good) {
        this.winGame();
      }
      if (this.$data.good == false) {
        this.flashColor();
        this.$data.counter = "NO";
        setTimeout(() => {
          this.reset();
          this.clearColor();
          this.$data.good = true;
          this.$data.intervalId = setInterval(this.gameTurn, 400);
        }, 400);
        this.$data.noise = false;
      }
      if (
        this.$data.turn == this.$data.playerOrder.length &&
        this.$data.good &&
        !this.$data.win
      ) {
        this.$data.turn++;
        this.reset();
        this.$data.intervalId = setInterval(
          this.gameTurn,
          this.$data.difficult
        );
      }
    },
    flashColor() {
      this.$data.styles[0].background = "lightgreen";
      this.$data.styles[1].background = "tomato";
      this.$data.styles[2].background = "yellow";
      this.$data.styles[3].background = "lightskyblue";
    },
    winGame() {
      this.flashColor();
      this.$data.counter = "WIN";
      this.$data.power = false;
      this.$data.win = true;
    },
  },
  data() {
    return {
      styles: [
        {
          background: "darkgreen",
          margin: "-250px 0px 0px -250px",
          borderRadius: "250px 0 0 0",
        },
        {
          background: "darkred",
          margin: "-250px 0px 0px 0px",
          borderRadius: "0 250px 0 0",
        },
        {
          background: "goldenrod",
          margin: "0px -250px 0px -250px",
          borderRadius: "0 0 0 250px",
        },
        {
          background: "darkblue",
          margin: "0px 0px -250px 0px",
          borderRadius: "0 0 250px 0",
        },
      ],
      noise: true,
      power: false,
      win: false,
      order: [],
      playerOrder: [],
      flash: 0,
      intervalId: false,
      compTurn: false,
      counter: "",
      turn: 0,
      good: null,
      difficult: 400,
    };
  },
};
</script>

<style scoped>
.difficult {
  position: absolute;
  top: 100px;
  right: 15%;
  z-index: 2;
  width: 300px;
  text-align: center;
  font-size: 1.5rem;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin-top: 20px;
  padding: 10px;
}
button {
  width: 7rem;
  height: 2rem;
  border-radius: 1rem;
  background-color: rgb(37, 85, 175);
  color: beige;
}
@media (max-width: 1400px) {
  .difficult {
    right: 100px;
  }
}
@media (max-width: 1200px) {
  .difficult {
    right: 0px;
  }
}
</style>
