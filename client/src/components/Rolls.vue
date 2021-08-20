<template>
  <div :key="roll.id" v-for="roll in rolls">
    <Roll @dice-rolled="$emit('dice-rolled', roll.title, roll.result, roll.success, roll.challenge)" @delete-roll="$emit('delete-roll', roll.id)" :roll="roll"/>
  </div>
</template>

<script>
import Roll from "./Roll";

export default {
  name: "Rolls",
  components: {
    Roll,
  },
  props: {
    rolls: Array,
  },
};
</script>