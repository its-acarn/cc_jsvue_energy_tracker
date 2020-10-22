<template>
  <section class="select-date-wrapper">
    <h2>Select Date</h2>
    <form v-on:submit.prevent='handleClick'>
      <div> <input type="datetime-local" required v-model="selectedDate" min="1000-01-10T00:00" max="9999-01-10T00:00" class="select-date-input"></div>
      <div><input type="submit" value="Select Date" class="select-date-submit-button"></div>
    </form>
  </section>
</template>

<script>
import {eventBus} from '../main.js';
export default {
  name: 'select-date',
  data() { 
    return {
      selectedDate: null
    }
  },
  methods: {
    handleClick ()  {
      eventBus.$emit('date-selected', this.selectedDate);
    }
  }
}
</script>

<style>
.select-date-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  margin-bottom: 3%;
}
.select-date-wrapper div {
  padding: 2%;
}

.select-date-submit-button {
  background-color: crimson;
  color: yellowgreen;
  width: 20ch;
  height: 4ch;
  font-size: large;
}

.select-date-submit-button:hover {
  background-color: magenta;
}

h2 {
  font-size: x-large;
  text-shadow: -4px 0 chartreuse, 0 4px chartreuse, 4px 0 chartreuse, 0 -4px chartreuse;
}

.select-date-input {
  width: 40ch;
  height: 5ch;
  font-size: large;
}
</style>
