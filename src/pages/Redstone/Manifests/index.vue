<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <h2>Manifest page</h2>
        <div v-for="(relayer, index) in relayers" :key="index" class="card mb-3">
          <div class="card-body">
            <h3 class="card-title">{{ relayer.chain.name }}</h3>
            <p class="card-text">Price feed: {{ relayer.priceFeeds }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      relayers: [],
    };
  },
  async created() {
    try {
      const response = await axios.get("http://localhost:4000/fetch-manifests");
      this.relayers = response.data;
    } catch (error) {
      console.error('Network Error:', error);
    }
  }
};
</script>

