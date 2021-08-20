<template>
  <form @submit="onSubmit" class="add-form" autocomplete="off">
    <div class="form-control">
      <label>Rolamento</label>
      <input
        type="text"
        name="diceString"
        v-model="diceString"
        placeholder="Insira um código. Ex: 3d6+2"
      />
      <input
        type="text"
        name="title"
        v-model="title"
        placeholder="Insira o título do rolamento"
      />
      <input
        type="text"
        name="challenge"
        v-model="challenge"
        placeholder="Insira o desafio do rolamento"
      />
      <input
        type="text"
        name="color"
        v-model="color"
        placeholder="Insira o código de uma cor"
      />
      <input type="submit" value="Salvar Rolamento" class="btn btn-block" />
    </div>
  </form>
</template>

<script>
export default {
  name: "AddRoll",
  data() {
    return {
      diceString: "",
      title: "",
      challenge: "",
      color: "",
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.diceString) {
        alert("Insira um código de rolamento.");
      } else if (!this.challenge) {
        alert("Insira 0 no desafio caso o CR não se aplique.");

      } else if (!this.title) {
        alert("Insira um título para o rolamento.")
      } else {
        if (!this.color) {
          this.color = "black";
        }
        const newRoll = {
          diceString: this.diceString,
          title: this.title,
          color: this.color,
          deleteable: true,
          challenge: parseInt(this.challenge),
        };
        this.$emit("add-roll", newRoll);
        this.diceString = "";
        this.title = "";
        this.color = "";
        this.challenge = null;
      }
    },
  },
};
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
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