<template>
  <div class=" col-span-full" v-if="news != null">
    <div class="py-4">
      <h1 class="dark:text-white font-bold text-2xl pb-1">
        {{ currentArticle.title }}
      </h1>
      <p class=" dark:text-white text-sm">{{ currentArticle.description }}</p>
      <p class=" dark:text-white text-xs">{{ currentArticle.source.name }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      news: null,
      currentIndex: 0,
      currentArticle: null,
      stop: false,
      show: true,
    };
  },
  created() {
    let api_key = process.env.VUE_APP_NEWS_API_KEY;
    var config = {
      method: "get",
      url: "https://newsapi.org/v2/top-headlines?country=us",
      headers: {
        "x-api-key": api_key,
      },
    };
    axios(config).then((news) => {
      this.news = news.data.articles;
      this.newsArticle();
    });
  },
  methods: {
    newsArticle: function() {
      let length = this.news.length;
      this.currentArticle = this.news[this.currentIndex];
      this.currentIndex++;
      setInterval(
        (function(scope) {
          return function() {
            scope.currentArticle = scope.news[scope.currentIndex];
            scope.currentIndex++;
            if (scope.currentIndex > length) scope.currentIndex = 0;
          };
        })(this),
        10000
      );
    },
  },
};
</script>

<style></style>
