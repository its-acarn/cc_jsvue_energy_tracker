<template lang='html'>
  <main id="energy-app">
    <div id="app-size">
      <h1>Energy Usage Tracker</h1>
      <select-date></select-date>
      <generate-chart :energyDetails='energyDetails'></generate-chart>
      <!-- <ul>
        <li></li>
      </ul> -->
      <!-- <chart-date></chart-date> -->
    </div>
  </main>
</template>

<script>
import {eventBus} from './main';
import selectDate from './components/selectDate.vue';
import generateChart from './components/generateChart.vue';

export default {
  name: 'App',
  data() {
    return {
      generationMix: [],
      selectedDate: null,
      energyDetails: null
    }
  },
  mounted () {
      eventBus.$on('date-selected', (date) => {
      this.selectedDate = date;
      const url = `https://api.carbonintensity.org.uk/generation/${this.selectedDate}Z/pt24h`;
      this.fetchURL(url);
      })
  },
  methods: {
      fetchURL: function (url) {
        fetch(url)
        .then(result => result.json())
        .then(generations => this.generationMix = generations)
        .then(() => this.convertData());
      },
      convertData: function () {
        this.energyDetails = this.generationMix['data'][0]['generationmix'].map(fuel => {return(Object.keys(fuel), Object.values(fuel))})
        this.energyDetails.sort()
        this.energyDetails.unshift(Object.keys(this.generationMix['data'][0]['generationmix'][0]))
      }
  },
  components: {
    'select-date': selectDate,
    'generate-chart': generateChart,

  }
  
}
</script>

<style lang='css'>

#energy-app {
  width: 100vw;
  display: flex;
  flex-flow: column;
  align-items: center;
}

#app-size {
  width: 80vw;
  text-align: center;
}

main > div > h1 {
  font-family: 'Red Hat Text', sans-serif;
  font-style: italic;
  text-decoration: underline; 
  color: blanchedalmond;
  font-weight: bold;
  font-size: 100px;
  text-shadow: -5px 0 black, 0 5px black, 5px 0 black, 0 -5px black;
  text-align: center;
}

.chart-buttons {
  display: flex;
  flex-flow: row;
  justify-content: space-evenly;
}

button {
  background-color: black;
  color: brown;
  border-radius: 5px;
  width: 20ch;
  height: 4ch;
  font-size: large;
  
}

button:hover {
  cursor: pointer;
  background-color: hotpink;
}
</style>
