<template>
  <v-navigation-drawer v-model="drawer" :clipped="$vuetify.breakpoint.lgAndUp" fixed app>
    <v-list dense>
      <template v-for="service in services">
        <v-layout v-if="service.heading" :key="service.heading" row align-center>
          <v-flex xs6>
            <v-subheader v-if="service.heading">
              {{ service.heading }}
            </v-subheader>
          </v-flex>
        </v-layout>
        <v-list-group v-else-if="service.children" :key="service.text" v-model="service.model" :prepend-icon="service.model ? service.icon : service['icon-alt']" append-icon="">
          <template v-slot:activator>
            <v-list-tile>
              <v-list-tile-content>
                <v-list-tile-title>
                  {{ service.text }}
                </v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </template>
          <v-list-tile v-for="(child, i) in service.children" :key="i" @click="">
            <v-list-tile-action v-if="child.icon">
              <v-icon>{{ child.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>
                {{ child.text }}
              </v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list-group>
        <v-list-tile v-else :key="service.text" @click="">
          <v-list-tile-action>
            <v-icon>{{ service.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>
              {{ service.text }}
            </v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </template>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    drawer: null,
    services: [
      { icon: 'contacts', text: 'ALPHA' },
      { icon: 'contacts', text: 'DEV' },
      { icon: 'contacts', text: 'QA' },
      { icon: 'contacts', text: 'PROD' }, {
        icon: 'keyboard_arrow_up',
        'icon-alt': 'keyboard_arrow_down',
        text: 'Applications',
        model: true,
        children: [
          { icon: 'vpn_key', text: 'service_a' }
        ]
      },
      { icon: 'settings', text: 'Settings' },
      { icon: 'help', text: 'Help' }
    ]
  })
}
</script>

<style scoped>
</style>
