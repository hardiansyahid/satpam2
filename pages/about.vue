<template>
  <h1>{{ title }}</h1>
  <img :src="data.url" v-if="data.url"/>
</template>

<script>
import axios from 'axios';
import { ref, onMounted } from 'vue';
import { useHead, useSeoMeta } from '#app';

export default {
  name: 'Home',
  setup() {
    const title = ref('About');
    const data = ref({});
    const list = ref([]);

    // Dynamic meta tags
    const setSeoMeta = () => {
      useHead({
        titleTemplate: 'About',
      });

      useSeoMeta({
        ogTitle: data.value.title,
        ogImage: data.value.url,
        ogDescription: data.value.title,
        googlebot: 'index, follow',
        description: 'Selamat datang di Satpam! Jelajahi dunia informasi dan layanan terlengkap untuk memenuhi segala kebutuhan Anda. Dari panduan praktis, tips dan trik, hingga berita terkini yang relevan, kami hadir untuk memberikan konten berkualitas yang menginspirasi. Dapatkan juga akses ke produk-produk inovatif, solusi bisnis, serta wawasan mendalam di berbagai bidang. Apapun yang Anda cari, Satpam adalah partner terpercaya untuk kesuksesan Anda. Mari bersama kami wujudkan impian dan tujuan Anda!',
        keywords: 'satpam,satpam2,nextsatpam',
      });
    };

    // Fetch data
    const getData = async () => {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/photos');
        list.value = response.data;
        data.value = response.data[0];

        // Set SEO meta tags dynamically after data is fetched
        setSeoMeta();
      } catch (error) {
        console.error(error);
      }
    };

    onMounted(() => {
      getData();
    });

    return {
      title,
      data,
      list,
    };
  },
};
</script>