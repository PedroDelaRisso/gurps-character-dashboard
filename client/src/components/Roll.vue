<template>
  <div>
    <b id="roll-title">{{ roll.title }}</b>
    <i id="roll-dice-string">{{ roll.diceString }}</i>
    <i v-if="this.roll.challenge !== 0" id="challenge-rating">
      – CR: {{ roll.challenge }}</i
    >
  </div>

  <div class="roll">
    <Button @click="rollDice()" :text="`Rolar`" :color="this.roll.color" />
    <h3 id="roll-result">{{ rollResult }}</h3>
    <i v-if="this.roll.challenge !== 0">
      <i
        id="fail-icon"
        v-if="!roll.success && rollResult !== 0"
        class="fas fa-times"
      ></i>
      <i
        id="success-icon"
        v-if="roll.success && rollResult !== 0"
        class="fas fa-check"
      ></i>
    </i>
    <i
      @click="onDelete(roll.id)"
      v-show="roll.deleteable"
      class="fas fa-times"
      id="delete-btn"
    ></i>
  </div>
</template>

<script>
import Button from "./Button";

export default {
  name: "Roll",
  components: {
    Button,
  },
  data() {
    return {
      rollResult: 0,
    };
  },
  props: {
    roll: Object,
  },
  methods: {
    rollDice() {
      this.rollResult = 0;
      let numberOfDice = parseInt(this.roll.diceString.split("d")[0]);
      let numberOfSides = parseInt(this.roll.diceString.split("d")[1]);
      let modifier;
      if (this.roll.diceString.includes("+")) {
        modifier = parseInt(this.roll.diceString.split("d")[1].split("+")[1]);
      } else if (this.roll.diceString.includes("-")) {
        modifier = parseInt(this.roll.diceString.split("d")[1].split("-")[1]);
      } else {
        modifier = 0;
      }
      for (let i = 0; i < numberOfDice; i++) {
        this.rollResult += Math.floor(
          Math.random() * numberOfSides + 1 + modifier
        );
      }
      this.roll.result = this.rollResult;

      if (this.roll.challenge > 0) {
        if (this.rollResult <= this.roll.challenge) {
          this.roll.success = true;
        } else {
          this.roll.success = false;
        }
        if (this.rollResult === 17 || this.rollRestul === 18)
          this.roll.success = false;
        if (this.rollResult === 3 || this.rollResult === 4) this.roll.success = true;
      }
      this.$emit(
        "dice-rolled",
        this.roll.title,
        this.roll.result,
        this.roll.success,
        this.roll.challenge
      );
    },
    onDelete(id) {
      this.$emit("delete-roll", id);
    },
  },
};
</script>

<style scoped>
#challenge-rating {
  color: #969696;
}

#fail-icon {
  color: #ce2828;
}

#success-icon {
  color: #72bd34;
}

#delete-btn {
  float: right;
  padding-top: 5px;
  color: red;
  cursor: pointer;
}

#roll-result {
  display: inline-block;
  background: #d2d9dd;
  color: #272727;
  margin: 5px;
  padding-top: 9px;
  text-align: center;
  width: 43px;
  height: 43px;
  line-height: 25px;
  font-size: 15px;
  border-radius: 5px;
}
#roll-dice-string {
  margin-left: 10px;
  color: #969696;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
  margin-left: 10px;
}

.roll {
  margin: 5px;
  padding: 10px 5px;
}
</style>