<template>

  <div class="card mb-4">
    <div class="card-body text-center">
      <h5 class="card-title">Random Dog Photo Using API</h5>
      <img v-if="dogImageUrl" :src="dogImageUrl" class="img-fluid rounded mb-3" alt="Random Dog" style="max-height: 300px;" />
      <p v-else>Loading dog photo...</p>
      <button @click="fetchDogPhoto" class="btn btn-primary d-block mx-auto mt-3">Get Another Dog Photo</button>
    </div>
  </div>
</template>

<script>
export default {

  name: 'DogPhoto', 
  data() {
    return {
      dogImageUrl: '' 
    };
  },
  methods: {
    async fetchDogPhoto() {
      
      try {
        const response = await fetch('https://dog.ceo/api/breeds/image/random');
        const data = await response.json(); 
        if (data.status === 'success') {
          this.dogImageUrl = data.message; 
        } else {
          this.dogImageUrl = ''; 
          console.error('Failed to fetch dog photo');
        }
      } catch (error) {
        this.dogImageUrl = ''; 
        console.error('Error fetching dog photo:', error);
      }
    }
  },
  mounted() {

    this.fetchDogPhoto();
  }
};
</script>

<style scoped>

.img-fluid {
  max-width: 100%;
  height: auto;
  border-radius: 1rem;
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.5);
   
}
</style>