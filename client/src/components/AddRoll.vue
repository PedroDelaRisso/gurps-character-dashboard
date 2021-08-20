<template>
  <form @submit="onSubmit" class="add-form" autocomplete="off">
    <div class="form-control">
      <label>Rolls</label>
      <input
        type="text"
        name="diceString"
        v-model="diceString"
        placeholder="Insert a roll code. Ex: '3d6+2'."
      />
      <input
        type="text"
        name="title"
        v-model="title"
        placeholder="Insert a title."
      />
      <input
        type="text"
        name="challenge"
        v-model="challenge"
        placeholder="Insert a challenge rating. 0 for no challenge."
      />
      <input
        type="text"
        name="color"
        v-model="color"
        placeholder="Insert a color code"
      />
      <input type="submit" value="Save roll" class="btn btn-block" />
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
  emits: ['add-roll'],
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.diceString) {
        alert("Insert a roll code.");
      } else if (!this.challenge) {
        alert("Insert a challenge rating. 0 if it doesn't apply");

      } else if (!this.title) {
        alert("Insert a title.")
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