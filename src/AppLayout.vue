<template>
  <v-app :style="{ background: $vuetify.theme.themes[theme].background }">
    <v-app-bar
      app
      dense
    >
      <slot name="appBar">
        <v-toolbar-title>Kanban Board</v-toolbar-title>
        <v-spacer></v-spacer>
          <v-switch
            v-model="darkTheme"
            label="Dark"
            hide-details
          ></v-switch>
        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </slot>
    </v-app-bar>

    <v-content>
      <slot></slot>
    </v-content>
  </v-app>    
</template>

<script>

export default {
  name: 'App',
  
  data: vm => ({
    darkTheme: vm.$vuetify ? vm.$vuetify.theme.dark : false,
  }),

  watch: {
    darkTheme() {
      this.$vuetify.theme.dark = this.darkTheme
    }
  },

  computed: {
    theme() {
      return (this.$vuetify.theme.dark) ? 'dark' : 'light'
    }
  },


  beforeDestroy () {
    if (!this.$vuetify) return
    this.$vuetify.theme.dark = this.darkTheme
  }
};
</script>
