<template>
  <h1>{{ title }}</h1>
  <img :src="data.url" v-if="data.url"/>
</template>

<script>
import axios from 'axios';
import { ref, watch } from 'vue';
import { useSeoMeta } from '#app';

export default {
  async setup() {
    const data = ref({});
    const title = ref('Home');

    const getData = async () => {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/photos');
        data.value = response.data[0];
      } catch (error) {
        console.error(error);
      }
    };

    // Fetch data before rendering
    await getData();

    // Watch for changes in data and update SEO meta tags when data is loaded
    watch(data, (newData) => {
      if (newData && newData.url) {
        useSeoMeta({
          ogTitle: newData.title,
          ogImage: newData.url,
          ogDescription: newData.title,
          googlebot: 'index, follow',
          description: 'Selamat datang di Satpam! Jelajahi dunia informasi dan layanan terlengkap untuk memenuhi segala kebutuhan Anda.',
          keywords: 'satpam,satpam2,nextsatpam',
        });
      }
    });

    return {
      data,
      title,
    };
  },
};
</script>
