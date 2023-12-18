<script lang="ts" setup>
defineProps({
  name: {
    type: String,
    required: true,
  },
});

const emit = defineEmits(["remove"]);
</script>

<template>
  <div class="card">
    <h4>{{ name }}</h4>
    <p @click="emit('remove')">x</p>
  </div>
</template>

<style scoped lang="scss">
.card {
  background: rgb(27, 60, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 0.1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
  p {
    position: absolute;
    top: -20%;
    left: 90%;
    cursor: pointer;
    color: white;
  }
}
</style>
