<template>
    <div id="container">
        <GChart :type="type" :data="picked" :options="options" />
        <div>
          <label>BTC</label>
            <input type="checkbox" ref="BTC" @change="updateChartData"/>
          <label>ETH</label>
            <input type="checkbox" ref="ETH" @change="updateChartData"/>
          <label>BCH</label>
            <input type="checkbox" ref="BCH" @change="updateChartData"/>
        </div>
    </div>
  </template>
  
  <script>
  import { GChart } from 'vue-google-charts';
  import cryptoData from '../../assets/crypto-data';
  export default {
    name: 'GoogleChart',
    components: {
      GChart,
    },
    data() {
      return {
        type: "LineChart",
        picked: [],
        options: 
        {  
          title: 'Crypto chart',
          curveType: 'function',
          legend: { position: 'bottom' },
          width: 1100,
          height: 700,
          colors: ['gold','purple','green'],
        },
        coins: [
          { ref: 'BTC', name: 'BTC' },
          { ref: 'ETH', name: 'ETH' },
          { ref: 'BCH', name: 'BCH' }
        ]
      };
    },
    methods: {
      updateChartData() {
        this.picked = [['Year']];
        for (let i = 0; i < cryptoData.length; i++){
          this.picked.push([cryptoData[i].year]);
        }
        this.coins.forEach((coin) => {
          if (this.$refs[coin.ref].checked) {
            this.picked[0].push(coin.name);
            for (let i = 0; i < cryptoData.length; i++){
              this.picked[i + 1].push(cryptoData[i][coin.name]);
            }
          }
        });
      },
    },
  }
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