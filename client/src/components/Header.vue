<template>
  <header>
    <h1>{{ title }}</h1>
    <Button @click="$emit('toggle-add-roll')" :text="showAddRoll ? 'Close' : 'Add Roll'" :color="showAddRoll ? 'red' : '#4DBD6B'"/>
  </header>
</template>

<script>
import Button from "./Button"
export default {
  name: "Header",
  components: {
      Button
  },
  props: {
    title: String,
    showAddRoll: Boolean
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>