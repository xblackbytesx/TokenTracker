<template>
  <section class="news">
    <header class="news-header">Latest News</header>
    <div class="news-block">
      <div class="news-item" v-for="(article, index) in news" :key="index">
        <figure class="news-item__thumb">
          <a :href="article.url" target="_blank">
            <img :src="article.imageurl" />
          </a>
        </figure>
        <div>
          <h6 class="news-item__title">
            <a :href="article.url" target="_blank">{{ article.title }}</a>
          </h6>
          <p v-html="truncateText(article.body)"></p>
          <div class="news-item__meta">
            <div class="news-source">{{ article.source_info.name }}</div>
            <div class="news-date">{{ article.published_on | time }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
// import * as timeago from "timeago.js";
export default {
  created() {
    this.getNews();
    this.interval = setInterval(
      function() {
        this.getNews();
      }.bind(this),
      120000
    );
  },
  beforeDestroy() {
    clearInterval(this.interval);
  },
  data() {
    return {
      news: [],
      interval: null
    };
  },
  methods: {
    truncateText(value) {
      if (value.length > 135) {
        const substr = value.substring(0, 135);
        return substr.substring(0, substr.lastIndexOf(" ")) + " ...";
      } else {
        return value;
      }
    },
    async getNews() {
      let response = await fetch(
        "https://min-api.cryptocompare.com/data/v2/news/?lang=EN"
      );
      if (response.ok) {
        let json = await response.json();
        this.news = json["Data"];
        console.log(json);
      } else {
        console.log("Fetch Error :-S", response.status);
      }
    }
  },
  filters: {
    time: function(value) {
      if (!value) return "";
      // return timeago().format(value * 1000);
    },
    tags: function(value) {
      if (!value) return "";
      return value.split("|").join(", ");
    }
  }
};
</script>
<style>
.news {
  height: 100%;
  line-height: 1.3;
  a,
  a:hover,
  a:active,
  a:focus {
    color: #007bff;
    text-decoration: none;
  }
  .news-header {
    text-align: center;
    height: 50px;
    line-height: 50px;
    font-size: 20px;
    font-weight: bold;
    background-color: #333;
    color: #ffde00;
    box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.05);
  }
}
.news-item {
  text-align: left;
  background: var(--bgcolor-z1);
  margin: 10px 15px 10px 10px;
  border-radius: 6px;
  border: 1px solid var(--border-z1);
  max-height: 200px;
  overflow: hidden;
  padding: 10px;

  p {
    font-size: 14px;
    line-height: 1.2;
    margin-bottom: 0.25rem;
  }

  &__thumb {
    margin: 0;
    padding: 0;
    float: left;
    max-width: 90px;
    margin-right: 10px;

    img {
      width: 90px;
      height: 90px;
      border-radius: 6px;
      display: block;
    }
  }

  &__title {
    font-size: 14px;
    font-weight: bold;
    margin-bottom: 0.25rem;
  }

  &__meta {
    display: block;
    font-size: 13px;
    color: #565656;
  }
}

.news-source {
  display: inline-block;
  color: orange;
}
.news-date {
  display: inline-block;
  float: right;
}
</style>
