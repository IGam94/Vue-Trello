<template>
  <div>
    <div v-if="loading">loading card...</div>
    <div v-else>Card
    <div>cid:{{cid}}</div></div>
  </div>
</template>

<script>
  export default {
    data(){
      return{
        cid:0,
        loading:false
      }
    },
    watch: {
      '$route' :{
        handler: 'fetchData',
        immediate: true
      }
    },
    methods: {
      fetchData(){
        this.loading = true
        setTimeout(() => {
          this.loading = false
          this.cid = this.$route.params.cid
        }, 500);
      }
    },

  }
</script>

<style>

</style>