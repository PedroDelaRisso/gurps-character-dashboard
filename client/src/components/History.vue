<template>
  <h1>Last 10 rolls</h1>
  <div class="history" :key="roll.id" v-for="roll in rolls">
    <p>
      <b class="roll-title">{{ roll.title }}:</b>
      <b class="roll-result">{{ roll.result }}</b>
      <i v-if="roll.challenge > 0">
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
    </p>
    <hr />
  </div>
</template>

<script>
import Roll from "./Roll";

export default {
  name: "History",
  components: {
    Roll,
  },
  props: {
    rolls: Array,
  },
};
</script>

<style scoped>
#fail-icon {
  color: #ce2828;
}

#success-icon {
  color: #72bd34;
}

.roll-title {
  margin-right: 10px;
}

.fas {
  float: right;
}
hr {
  border-color: rgb(121, 121, 121);
}
</style>