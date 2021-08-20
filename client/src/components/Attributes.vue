<template>
  <h1>Attributes</h1>
  <form class="form-control">
    <label for="st">Força (ST):</label>
    <input v-model="st" @change="changeAttribute(0, st)" type="number" />
    <label for="st">Destreza (DX):</label>
    <input v-model="dx" @change="changeAttribute(1, dx)" type="number" />
    <label for="st">Inteligência (IQ):</label>
    <input v-model="iq" @change="changeAttribute(2, iq)" type="number" />
    <label for="st">Constituição (HT):</label>
    <input v-model="ht" @change="changeAttribute(3, ht)" type="number" />
  </form>
  <div class="attribute-rolls" :key="roll.id" v-for="roll in rolls">
    <Roll
      @dice-rolled="$emit('dice-rolled', roll.title, roll.result, roll.success, roll.challenge)"
      :roll="roll"
    />
  </div>
</template>

<script>
import Roll from "./Roll";
import Button from "./Button";

export default {
  name: "Attributes",
  components: {
    Roll,
    Button,
  },
  emits: ['dice-rolled'],
  data() {
    return {
      st: Number,
      dx: Number,
      iq: Number,
      ht: Number,
      rolls: [],
    };
  },
  methods: {
    async changeAttribute(id, value) {
      const attributeToChange = await this.fetchAttribute(id);
      const updatedAttribute = { ...attributeToChange, challenge: value };

      const res = await fetch(`api/attributes/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updatedAttribute),
      });

      const data = await res.json();

      this.rolls = this.rolls.map((roll) =>
        roll.id === id ? { ...roll, challenge: data.challenge }
        : roll
      );
    },
    async fetchAttributes() {
      const res = await fetch("api/attributes");

      const data = await res.json();

      return data;
    },
    async fetchAttribute(id) {
      const res = await fetch(`api/attributes/${id}`);

      const data = await res.json();

      return data;
    },
    async getAttributeLevel(id) {
      const selectedAttribute = await this.fetchAttribute(id);
      return selectedAttribute.challenge;
    }
  },
  async created() {
    this.rolls = await this.fetchAttributes();
    this.st = this.rolls[0].challenge;
    this.dx = this.rolls[1].challenge;
    this.iq = this.rolls[2].challenge;
    this.ht = this.rolls[3].challenge;
  },
};
</script>

<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input[type="number"] {
  -moz-appearance: textfield;
}

label {
  margin-bottom: 15px;
}

.attribute-rolls {
  padding-top: 15px;
}

.fas {
  font-size: 10pt;
  float: left;
}

.form-control {
  margin: 20px 0;
  padding-top: 3px;
  float: left;
}

.form-control label {
  display: block;
}

.form-control input {
  text-align: center;
  width: 50px;
  height: 40px;
  margin: 0 130px 43px 10px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>