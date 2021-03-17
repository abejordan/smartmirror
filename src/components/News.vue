<template>
  <div class="border col-span-full">
    <div v-for="(index, article) in news" :key="article.url">
    <h1 class="dark:text-white">{{article.title}}</h1>
    <p>{{article.content}}</p>
    <p>{{article.source}}</p>
    </div>
  </div>
</template>

<script>
//import axios from "axios";
export default {
  data(){
    return{
      news:null
    }
  },
/*   created() {
    let api_key = process.env.VUE_APP_NEWS_API_KEY;
    var config = {
  method: 'get',
  url: 'http://api.datanews.io/v1/headlines',
  headers: { 
    'x-api-key': api_key
  }
};
      axios(config)
      .then((news) => {
        this.news = news.data.hits;
      });
  }, */
};
</script>

<style></style>
