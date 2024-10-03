<template>
  <h1>{{ title }}</h1>
  <img :src="data.url" v-if="data.url"/>
</template>

<script>
import axios from 'axios';
import { ref, onMounted } from 'vue';
import { useHead, useSeoMeta } from '#app';

export default {
  async setup() {
    const data = ref({});

    const getData = async () => {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/photos');
        data.value = response.data[0];

        // Set SEO meta tags after data is fetched
        useSeoMeta({
          ogTitle: data.value.title,
          ogImage: data.value.url,  // Make sure this URL is accessible
          ogDescription: data.value.title,
          googlebot: 'index, follow',
          description: 'Dukung pengawasan layanan publik bebas korupsi.',
          keywords: 'jaga, kpk, jaga kpk, layanan publik',
        });
      } catch (error) {
        console.error(error);
      }
    };

    // Fetch data before rendering
    await getData();

    return {
      data,
    };
  },
};

</script>