<template>
    <div>
      <p>Counter: {{ counter }}</p>
      <button @click="increment">Increment</button>
      <button @click="decrement">Decrement</button>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup() {
    
    // Using ref to create reactive state
    const counter = ref(0);
    
    // Function to increment the counter
    const increment = () => {
      counter.value += 1;
    };
    
    // Function to decrement the counter
    const decrement = () => {
      counter.value -= 1;
    };
    // Exposing data and methods to the template
    return {
        counter,
        increment,
        decrement,
        
      };
    },
  };
  </script>