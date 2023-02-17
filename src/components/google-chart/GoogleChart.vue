<template>
    <div id="container">
        <GChart :type="type" :data="data" :options="options" />
        <div>
            <input type="checkbox" checked v-model="one" @change="updateChartData"/>
            <input type="checkbox" v-model="two" @change="updateChartData"/>
            <input type="checkbox" v-model="three" @change="updateChartData"/>
        </div>
    </div>
  </template>
  
  <script>
  import { GChart } from 'vue-google-charts';
  
  export default {
    name: 'GoogleChart',
    components: {
      GChart,
    },
    data() {
      return {
        type: "LineChart",
        data: [],
        options: 
        {  
            title: 'Crypto Prices',
            curveType: 'function',
            legend: { position: 'bottom' },
            width: 1100,
            height: 700,
        },
        one: true,
        two: false,
        three: false
      };
    },
    computed: {

    },
    methods: {
    updateChartData() {
        this.data = [['Year']];
            const years = ['2018', '2019', '2020', '2021'];

            if (this.one) {
                this.data[0].push('one')
                this.data.push([years[0], 500]); // example one data for year 2018
                this.data.push([years[1], 800]); // example one data for year 2019
                this.data.push([years[2], 1000]); // example one data for year 2020
                this.data.push([years[3], 3500]); // example one data for year 2021
            }

            if (this.two) {
                this.data[0].push('two')
                this.data[1].push(991); // example two data for year 2018
                this.data[2].push(550); // example two data for year 2019
                this.data[3].push(993); // example two data for year 2020
                this.data[4].push(555); // example two data for year 2021
            }

            if (this.three) {
                this.data[0].push('three')
                this.data[1].push(1003); // example three data for year 2018
                this.data[2].push(730); // example three data for year 2019
                this.data[3].push(500); // example three data for year 2020
                this.data[4].push(1980); // example three data for year 2021
            }
            if(this.data === ['year']){
                this.data = []
            }

        }
      // trigger chartData computed property update
    },
    
  };
  </script>
  
  <style scoped>

    #container{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        width: 100vw;
    }

</style>