<template>
  <v-footer color="green darken-1">
    <v-card flat tile width="100%" class="darken-1 green text-center">
      <v-card-text>
        <v-row justify="center">
          <div v-for="icon in icons" v-bind:key="icon.url">
            <v-icon @click="select(icon)">{{ icon.icon }}</v-icon>
            &nbsp; &nbsp;
          </div>
        </v-row>
      </v-card-text>

      <v-divider></v-divider>

      <v-card-text class="white--text">
        {{ new Date().getFullYear() }} —
        <strong>Jack Whisler</strong>
      </v-card-text>
    </v-card>
  </v-footer>
</template>

<script>
/* eslint-disable prettier/prettier */

export default {
  name: "App",

  data: () => ({
    icons: [
      { icon: "fa-github", url: "https://github.com/jackwhisler1/drum-machine" },
      { icon: "fa-linkedin", url: "https://www.linkedin.com/in/jackwhisler/" },
      { icon: "fa-solid fa-envelope", url: "https://jackwhisler1.github.io/" },
    ],
  }),
  methods: {
    select: function (icon) {
      window.location.href = icon.url;
    },
  },
};
</script>
