<template>
  <h1>Last 10 rolls</h1>
  <div class="history" :key="roll.id" v-for="roll in rolls">
    <p>
      <i>{{ roll.title }}:</i> <b>{{ roll.result }}</b>
    </p>
  </div>
</template>

<script>
import Roll from "./Roll";

export default {
  name: "History",
  components: {
    Roll
  },
  props: {
    rolls: Array,
  },
};
</script>

<style scoped>
i {
    font-size: 11pt;
}
</style>