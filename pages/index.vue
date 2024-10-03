<template>
  <div>
    <h1>{{ article.title }}</h1>
    <img :src="article.url" v-if="article.url" alt="Article Image" />
  </div>
</template>

<script>
import axios from 'axios';

export default {
  // Mengambil data sebelum halaman dirender
  async asyncData({ params }) {
    // Gantikan URL dengan endpoint API yang benar
    const { data } = await axios.get('https://jsonplaceholder.typicode.com/photos/1');
    return {
      article: data, // Simpan data artikel yang diambil di state
    };
  },

  // Mengatur meta tags di server
  head() {
    return {
      title: this.article.title, // Gunakan judul dari artikel
      meta: [
        { hid: 'description', name: 'description', content: this.article.title },
        { hid: 'og:title', property: 'og:title', content: this.article.title },
        { hid: 'og:description', property: 'og:description', content: this.article.title },
        { hid: 'og:image', property: 'og:image', content: this.article.url },
        { hid: 'og:url', property: 'og:url', content: `https://satpam2-tau.vercel.app/articles/${this.article.id}` },
      ],
    };
  },
};
</script>
