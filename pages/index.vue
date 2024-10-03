<template>
  <h1>{{title}}</h1>
</template>

<script>
useHead({
  titleTemplate: 'Home Page',
})
useSeoMeta({
  googlebot: true,
  description : 'Dukung pengawasan layanan publik bebas korupsi. Tingkatkan transparansi pemerintah dengan partisipasi Anda. Kenali upaya pencegahan korupsi KPK di sini.',
  keywords:"jaga, kpk, jaga kpk, jaringan pencegahan korupsi, kpk jaga, pelayanan publik, jaga pendidikan, jaga kesehatan, dana desa"
})
export default {
  name: 'Home',
  data(){
    return {
      title : 'Home',
    }
  }
}
</script>