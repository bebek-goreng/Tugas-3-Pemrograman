<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>CryptoCurrency</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <div class="button-container">
        <ion-button @click="fetchCryptoData" color="primary">Refresh</ion-button>
      </div>
      <ion-grid v-if="cryptocurrencies.length > 0" class="table-container">
        <ion-row class="table-header">
          <ion-col>Rank</ion-col>
          <ion-col>Name</ion-col>
          <ion-col>Symbol</ion-col>
          <ion-col>Price (USD)</ion-col>
        </ion-row>
        <ion-row v-for="crypto in cryptocurrencies" :key="crypto.id" class="table-row">
          <ion-col>{{ crypto.rank }}</ion-col>
          <ion-col>{{ crypto.name }}</ion-col>
          <ion-col>{{ crypto.symbol }}</ion-col>
          <ion-col>{{ crypto.price_usd }}</ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';

export default defineComponent({
  name: 'Home',
  data() {
    return {
      cryptocurrencies: []
    };
  },
  methods: {
    async fetchCryptoData() {
      try {
        const response = await axios.get('https://api.coinlore.net/api/tickers/');
        this.cryptocurrencies = response.data.data;
      } catch (error) {
        console.error('Error fetching cryptocurrency data:', error);
      }
    }
  }
});
</script>

<style scoped>
.button-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.table-container {
  width: 100%;
  margin-top: 20px;
}

.table-header {
  font-weight: bold;
  border-bottom: 2px solid #ccc;
  padding: 10px 0;
}

.table-row {
  border-bottom: 1px solid #eee;
}

ion-col {
  padding: 10px;
  text-align: center;
}

ion-row {
  align-items: center;
}
</style>
