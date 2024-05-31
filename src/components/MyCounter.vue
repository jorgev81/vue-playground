<script setup>
import { reactive } from 'vue';

/* Reactive only works with non primitives data types like array or objects */
const state = reactive({
  count: 0
});

const increment = () => {
  state.count++;
};

const decrement = () => {
  state.count--;
};


</script>

<template>
  <div>
    <p>Counter: {{ state.count }}</p>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
  </div>
</template>