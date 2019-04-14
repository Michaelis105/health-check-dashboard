<template>
  <v-card :color=service.color>
    <v-card-title primary-title>
      <div>
        <h3 class="headline mb-0">{{ service.name }}</h3>
        <h5>{{ service.status }}</h5>
        <h5>{{ service.reason }}</h5>
      </div>
    </v-card-title>
    <v-card-actions>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "ServiceItem",
  props: ["service"]
}
</script>

<style scoped>
</style>
