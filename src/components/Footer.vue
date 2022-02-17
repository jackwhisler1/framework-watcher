<template>
  <v-footer class="lighten-1 green text-center">
    <v-card flat tile width="100%" class="lighten-1 green text-center">
      <v-card-text>
        <v-row justify="center">
          <div>
            <v-icon class="p-2" v-for="icon in icons" v-bind:key="icon.url" @click="select(icon)">
              {{ icon.icon }}
            </v-icon>
          </div>
        </v-row>
      </v-card-text>

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
      { icon: "fa-github", url: "https://github.com/jackwhisler1" },
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
