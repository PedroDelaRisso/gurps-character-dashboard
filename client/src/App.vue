<template>
  <div class="container">
    <Header
      @toggle-add-roll="toggleAddRoll"
      title="Rolls"
      :showAddRoll="showAddRoll"
    />
    <div v-if="showAddRoll">
      <AddRoll @add-roll="addRoll" />
    </div>
    <Rolls
      @dice-rolled="addToHistory"
      @delete-roll="deleteRoll"
      :rolls="rolls"
    />
    <br />
    <Attributes @dice-rolled="addToHistory" @rolled-attribute="rollAttribute" />
  </div>
  <div class="container">
    <History :rolls="rollHistory" />
  </div>
</template>

<script>
import Header from "./components/Header";
import Button from "./components/Button";
import Rolls from "./components/Rolls";
import AddRoll from "./components/AddRoll";
import History from "./components/History";
import Attributes from "./components/Attributes";

export default {
  name: "App",
  components: {
    Header,
    Button,
    Rolls,
    AddRoll,
    History,
    Attributes,
  },
  data() {
    return {
      rolls: [],
      rollHistory: [],
      showAddRoll: false,
    };
  },
  methods: {
    async addRoll(roll) {
      const res = await fetch("api/rolls", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(roll),
      });

      const data = await res.json();

      this.rolls = [...this.rolls, data];
    },
    addToHistory(title, result) {
      if (this.rollHistory.length < 10) {
        this.rollHistory = [{ title, result }, ...this.rollHistory];
      } else {
        this.rollHistory.splice(9, 1);
        this.rollHistory = [{ title, result }, ...this.rollHistory];
      }
    },
    async deleteRoll(id) {
      if (confirm("Tem certeza?")) {
        const res = await fetch(`api/rolls/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.rolls = this.rolls.filter((roll) => roll.id !== id))
          : alert("Erro ao deleter rolamento.");
      }
    },
    toggleAddRoll() {
      this.showAddRoll = !this.showAddRoll;
    },
    toggleHistory() {
      this.showHistory = !this.showHistory;
    },
    rollAttribute(attr) {
      this.rolls[0].challenge = attr;
    },
    async fetchRolls() {
      const res = await fetch("api/rolls");

      const data = await res.json();

      return data;
    },
    async fetchRoll(id) {
      const res = await fetch(`api/rolls/${id}`);

      const data = await res.json();

      return data;
    },
  },
  async created() {
    this.rolls = await this.fetchRolls();
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-color: rgb(47, 49, 54);
  font-family: "Poppins", sans-serif;
  color: #e4e4e4;
}

input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus,
textarea:-webkit-autofill,
textarea:-webkit-autofill:hover,
textarea:-webkit-autofill:focus,
select:-webkit-autofill,
select:-webkit-autofill:hover,
select:-webkit-autofill:focus {
  caret-color: rgb(215, 214, 217);
  box-shadow: 0 0 0px 1000px rgb(64, 68, 75) inset;
  -webkit-text-fill-color: rgb(215, 214, 217);
}

input {
  background-color: rgb(64, 68, 75);
  border: none;
  border-radius: 5px;
  color: rgb(215, 214, 217);
}

input::placeholder {
  color: rgb(112, 117, 125);
}

input:focus,
input:active {
  outline: none;
}

.container {
  background-color: rgb(54, 57, 63);
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  transition: 220ms;
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn:hover {
  transition: 220ms;
  box-shadow: 0 0 0px 1000px rgba(255, 255, 255, 0.1) inset;
}

.btn-block {
  display: block;
  width: 100%;
}
</style>