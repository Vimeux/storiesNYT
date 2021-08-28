<template>
  <Layout>
    <h2 class="layout-title">
      News Section : <span class="layout-title-section">{{ section }}</span>
    </h2>
    <NewsFilter v-model="section" :fetch="fetchNews" />
    <NewsList v-if="!loading && !error" :posts="posts" />

    <!-- animation de chargement -->
    <div class="loading" v-if="loading">
      <h3 class="loading-message">Loading...</h3>
    </div>
    <!-- fin animation de chargement -->

    <!-- message d'erreur -->
    <div class="error" v-if="error">
      <h3 class="error-title">
        {{ error.title }}
      </h3>
      <p class="error-message">{{ error.message }}</p>
    </div>
    <!-- fin message d'erreur -->
  </Layout>
</template>

<script>
import Layout from "./components/Layout.vue";
import NewsFilter from "./components/NewsFilter.vue";
import NewsList from "./components/NewsList.vue";

import axios from "axios";
const api = "N07Y48Kecv3qjvD7RJHFzU8lCDnJ78K6";

export default {
  components: {
    Layout,
    NewsFilter,
    NewsList,
  },
  data() {
    return {
      section: "arts",
      posts: [],
      loading: false,
      error: null,
    };
  },
  methods: {
    // Helper function pour récupérer l'image
    extractImage(post) {
      const defaultImg = {
        url: "http://placehold.it/210x140?text=N/A",
        caption: post.title,
      };
      if (!post.multimedia) {
        // si il n'y a pas de multimédia
        return defaultImg;
      }
      let imgObj = post.multimedia.find(
        (media) => media.format === "mediumThreeByTwo210" //définit le format de l'image
      );
      return imgObj ? imgObj : defaultImg; //si le format est présent on affiche l'image sinon on met une image basique.
    },
    async fetchNews() {
      //création fonction asynchrone pour récupérer les données
      try {
        this.error = null;
        this.loading = true;
        const url = `https://api.nytimes.com/svc/topstories/v2/${this.section}.json?api-key=${api}`; //url de l'API, la section est mise en variable
        const response = await axios.get(url); //requete à l'API avec axios
        const results = response.data.results; //récupere les résultat
        this.posts = results.map((post) => ({
          // parcours les donnée et les reformates et les rentre dans notre variable posts
          title: post.title,
          abstract: post.abstract,
          url: post.url,
          thumbnail: this.extractImage(post).url, //récupere l'image grâce à la fonction extractImage
          caption: this.extractImage(post).caption,
          byline: post.byline,
          published_date: post.published_date,
        }));
      } catch (err) {
        //si la récupératon se passe mal, on affiche une erreur
        if (err.response) {
          // erreur serveur (5xx, 4xx)
          this.error = {
            title: "Server Response",
            message: err.message,
          };
        } else if (err.request) {
          // le client ne recoit pas de réponse, ou la demande n'est jamais partie (erreur réseaux)
          this.error = {
            title: "Unable to Reach Server",
            message: err.message,
          };
        } else {
          // les erreurs diverses (dans le code par exemple)
          this.error = {
            title: "Application Error",
            message: err.message,
          };
        }
      }
      this.loading = false;
    },
  },
  mounted() {
    this.fetchNews();
  },
};
</script>

<style lang="scss">
@import "./assets/css/variable";

body {
  margin: 0;
  font-family: $text;
}
p {
  margin: 0;
}
.layout-title {
  margin: 0;
  padding: 1rem;
  font-family: $text;
  font-weight: 600;
  font-size: 30px;
  text-align: center;
  &-section {
    color: $color2;
    text-transform: capitalize;
  }
}
.error {
  height: 90vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  &-title {
    color: $color1;
    font-size: 40px;
  }
  &-message {
    color: $color1;
    font-size: 30px;
  }
}
.loading {
  height: 90vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  &-message {
    color: $color5;
    font-size: 50px;
    animation: 3s ease-in-out 1s infinite reverse both running loading;
  }
}

@keyframes loading{
  from{
    transform: scale(1);
    color: $color5;
  }
  50%{
    transform: scale(1.2);
    color: $color4;
  }
  to{
    transform: scale(1);
    color: $color5;
  }
}
</style>
