<template>
  <v-content>
    <v-container fluid grid-list-xl>
      <v-layout justify-start align-start wrap>
        <v-flex v-for="service in services" :key="services.name" xs6 sm3 md3 lg3>
          <ServiceItem v-if="service.healthCheckUrl != null" v-bind:color="service.color" v-bind:service="service" v-bind:text="service.status" />
        </v-flex>
      </v-layout>
    </v-container>
  </v-content>
</template>

<script>
import axios from 'axios';
import services from '../../assets/services.json';
import ServiceItem from '../ServiceItem';

const statuses = {
  HEALTHY: {
    color: "green darken-1",
    textColor: "white",
    text: "Healthy"
  },
  UNHEALTHY: {
    color: "yellow darken-1",
    textColor: "black",
    text: "Unhealthy"
  },
  CRITICAL: {
    color: "red darken-1",
    textColor: "white",
    text: "Critical"
  },
  UNKNOWN: {
    color: "grey lighten-1",
    textColor: "white",
    text: "Unknown"
  }
}

export default {
  name: "Content",
  components: {
    ServiceItem
  },

  computed: {
    services() {
      return services.services;
    }
  },

  data() {
    return {
      response: null,
      errorReason: null
    }
  },

  methods: {

    getResponse: function(url) {
      axios.get(url).then(response => {
        this.response = response
      }).catch(error => {
        console.log(error)
        this.errorReason = error
      })
    },

    healthCheck: function(name, url) {
      //console.log("- Health check service " + name + " at " + url);

      //this.getResponse(url);
      console.log(this.errorReason);
      if (!this.response) {
        return statuses.CRITICAL;
      }

      // TODO: Evaluate response here
      return statuses.UNKNOWN;
    },

    healthCheckAll: function() {
      console.log("--------------------------------------------");
      console.log("Performing health check on all services...");

/*
      for (var i = 0; i < this.services.length; i++) {
        var serviceName = this.services[i].name;
        var healthCheckUrl = this.services[i].healthCheckUrl;
        var service = services.services.find(function(item) {
          return item.name == serviceName
        });
        if (healthCheckUrl && healthCheckUrl != 'undefined') {
          var status = this.healthCheck(serviceName, healthCheckUrl);
          console.log(this.response);
          switch (status) {
            case statuses.HEALTHY:
              service.color = statuses.HEALTHY.color;
              service.status = statuses.HEALTHY.text;
              break;
            case statuses.UNHEALTHY:
              service.color = statuses.UNHEALTHY.color;
              service.status = statuses.UNHEALTHY.text;
              service.reason = this.errorReason;
              break;
            case statuses.CRITICAL:
              service.color = statuses.CRITICAL.color;
              service.status = statuses.CRITICAL.text;
              service.reason = this.errorReason;
              break;
            case statuses.UNKNOWN:
              service.color = statuses.UNKNOWN.color;
              service.status = statuses.UNKNOWN.text;
              service.reason = "UNIMPLEMENTED";
              break;
            default:
              //console.log(status);
              console.log("- Unknown status for service " + serviceName);
          }
        } else {
          service.color = statuses.UNKNOWN.color;
          service.status = statuses.UNKNOWN.text;
          service.reason = "Undefined health check endpoint";
        }
      }
      */

      console.log("Done health check on all services...");
    },
  },

  created: function() {
    console.log("Found " + this.services.length + " services to perform health check on...");
    this.healthCheckAll();
    setInterval(function() {
      this.healthCheckAll();
    }.bind(this), 10000);
  }
}
</script>

<style scoped>
</style>
