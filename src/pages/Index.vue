<template>
  <q-page>
    <div class="q-gutter-md" style="max-width: 300px">
      <q-list v-for="(cliente,index) in clientes" v-bind:key="index" bordered separator v-show="true"  style="margin: 0px 16px">
        <transition appear enter-active-class="animated fadeIn" leave-active-class="animated fadeOut">
          <q-item clickable>
            <q-item-section> Nome: {{ cliente.name }} </q-item-section>
          </q-item>
        </transition>
      </q-list>
      <q-btn
       @click="loadData"
       color="primary" label="Primary" />
    </div>
  </q-page>
</template>

<script>
import { openURL, Quasar, QSelect } from 'quasar';
import Vue from 'vue';
import axios from 'axios';

Vue.prototype.$axios = axios

const endPoint = 'http://127.0.0.1:8000/api/v1/clientes/?format=json'
const HTTPClient = axios.create({
  baseURL: endPoint
})


var invocation = new XMLHttpRequest();

HTTPClient.defaults.xsrfCookieName = 'csrftoken'
HTTPClient.defaults.xsrfHeaderName = 'X-CSRFToken'


export default {
  data () {
    return {
      clientes: {},
    }
  },
  methods: {
    loadData() {
      this.$axios.get(endPoint, {
        headers: {
          'Access-Control-Allow-Origin' : '*',
          'Access-Control-Allow-Methods' : 'GET, POST, PUT, PATCH, POST, DELETE, OPTIONS, REDIRECT',
          'Access-Control-Allow-Headers': "x-requested-with, Content-Type, origin, authorization, accept, client-security-token",
        }
      })
      .then((response) => {
        this.data = response.data
        console.log(this.data)
      })
      .catch(() => {
        this.$q.notify({
          color: 'negative',
          position: 'top',
          message: 'Loading failed',
          icon: 'report_problem'
      })
    })
    },
    listClient ({ commit }) { 
      console.log('CLientes')
      return new Promise((resolve, reject) => {
        HTTPClient.get('/api/v1/clientes/?format=json')
    })
  }
}
}
</script>
