<template>
  <v-toolbar :clipped-left="$vuetify.breakpoint.lgAndUp" color="grey darken-3" dark app fixed>
    <v-toolbar-title style="width: 300px" class="ml-0 pl-3">
      <!--<v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>-->
      <span id="dashboardTitle" class="hidden-sm-and-down">Health Check</span>
    </v-toolbar-title>
    <v-spacer></v-spacer>
    <v-btn color="grey darken-1">
      <v-icon left>assessment</v-icon>
      Health Check
    </v-btn>
    <v-btn color="grey darken-1">
      <v-icon left>settings_applications</v-icon>
      Application Control
    </v-btn>
    <v-spacer></v-spacer>
    <v-btn icon>
      <v-icon>phone</v-icon>
    </v-btn>
    <v-btn icon>
      <v-icon>settings</v-icon>
    </v-btn>
  </v-toolbar>
</template>

<script>
export default {
  name: "Toolbar"

  /*
  props: {
    sideBarId: {
        type: String,
        required: true
    }
  }
  */
}
</script>

<style scoped>
#dashboardTitle {
  font-weight: 600;
}
</style>
