<template>
  <div>
    <h2><strong>Understanding Emit</strong></h2>
    <button @click="$emit('counterEvent', 6)">Click Me</button>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Counter",
};
</script>

<style></style>
