<template>
  <h1>{{title}}</h1>
  <img :src="data.url"/>
</template>

<script>
import axios from 'axios';

useHead({
  titleTemplate: 'Home Page',
})
useSeoMeta({
  ogTitle:this.data.title,
  ogImage: this.data.url,
  ogDescription:this.data.title,
  googlebot: 'index, follow',
  description : 'Dukung pengawasan layanan publik bebas korupsi. Tingkatkan transparansi pemerintah dengan partisipasi Anda. Kenali upaya pencegahan korupsi KPK di sini.',
  keywords:"jaga, kpk, jaga kpk, jaringan pencegahan korupsi, kpk jaga, pelayanan publik, jaga pendidikan, jaga kesehatan, dana desa"
})
export default {
  name: 'Home',
  data(){
    return {
      title : 'Home',
      data : {}
    }
  },
  mounted() {
    axios.get('https://jsonplaceholder.typicode.com/photos')
    .then(response => {
      this.data = response.data[0];
    }).catch(reason => {
      console.log(reason);
    })
  }
}
</script>