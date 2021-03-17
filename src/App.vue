<template>
  <div id="app">
    <div class="columns is-mobile is-centered">
      <div class="column is-half">
        <p class="bd-notification is-primary">
          <input
            class="input is-rounded"
            type="text"
            placeholder="@GitHubAccount here ..."
          />
          <button
            @click="searchAction"
            id="searchButton"
            class="button is-rounded"
          >
            Search
          </button>
        </p>
        <div class="box">
          <article class="media">
            <div class="media-left">
              <figure class="image is-64x64">
                <img
                  :src="profile.ava"
                  alt="Image"
                />
              </figure>
            </div>
            <div class="media-content">
              <div class="content">
                <p>
                  <strong>John Smith</strong> <small>@johnsmith</small>
                  <small>31m</small>
                  <br />
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit.
                  Aenean efficitur sit amet massa fringilla egestas. Nullam
                  condimentum luctus turpis.
                </p>
              </div>
              <nav class="level is-mobile">
                <div class="level-left">
                  <a class="level-item" aria-label="reply">
                    <span class="icon is-small">
                      <i class="fas fa-reply" aria-hidden="true"></i>
                    </span>
                  </a>
                  <a class="level-item" aria-label="retweet">
                    <span class="icon is-small">
                      <i class="fas fa-retweet" aria-hidden="true"></i>
                    </span>
                  </a>
                  <a class="level-item" aria-label="like">
                    <span class="icon is-small">
                      <i class="fas fa-heart" aria-hidden="true"></i>
                    </span>
                  </a>
                </div>
              </nav>
            </div>
          </article>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      input: "",
      url: `https://api.github.com/users/${this.input}`,
      profile: {
        followers: "",
        following: "",
        avatar: "",
        email: "",
        bio: "",
      },
      error: "",
    };
  },
  methods: {
    searchAction: async function () {
      await axios
        .get(this.url)
        .then((res) => {
          this.profile.followers = res.data.followers;
          this.profile.following = res.data.following;
          this.profile.avatar = res.data.avatar_url;
          this.profile.email = res.data.email;
          this.profile.bio = res.data.bio;
        })
        .catch((error) => {
          this.error = error;
          console.log(error);
        });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 350px;
}

#searchButton {
  margin-top: 10px;
}
</style>
