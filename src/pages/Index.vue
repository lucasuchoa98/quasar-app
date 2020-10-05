<template>
  <q-page class="block">
      <q-list v-for="(form,index) in livros" v-bind:key="index" bordered separator v-show="true"  style="margin: 0px 16px">
        <transition appear enter-active-class="animated fadeIn" leave-active-class="animated fadeOut">
          <q-item clickable>
            <q-item-section>{{index}}</q-item-section>
            <q-item-section>{{livros[index]}}</q-item-section>
            <q-item-section><q-btn push color="primary" label="Push" /></q-item-section>
          </q-item>
        </transition>
      </q-list>
    {{data}}
  </q-page>
</template>

<script>
import { openURL } from 'quasar';
import Vue from 'vue';
import axios from 'axios';

Vue.prototype.$axios = axios

const endPoint = 'http://127.0.0.1:8000/api/v1/clientes'
const HTTPClient = axios.create({
  baseURL: endPoint
})


var invocation = new XMLHttpRequest();

function requestApi () {
  if (invocation){
    invocation.open('GET', endPoint, true);
    invocation.onreadystatechange =  handler;
    invocation.send()
  }
}

HTTPClient.defaults.xsrfCookieName = 'csrftoken'
HTTPClient.defaults.xsrfHeaderName = 'X-CSRFToken'

const listClient = ({ commit }) => { 
    console.log('CLientes')
    return new Promise((resolve, reject) => {
      HTTPClient.get('/api/v1/clientes')
    })
    
}

export default {
  data () {
    return {
      livros: data,
      alert: false,
      apiData: {}
    }
  },
  methods: {
    loadData() {
      this.$axios.get('https://jsonplaceholder.typicode.com/todos/1')
      .then((response) => {
        this.data = response.data
      })
      .catch(() => {
        this.$q.notify({
          color: 'negative',
          position: 'top',
          message: 'Loading failed',
          icon: 'report_problem'
      })
    })
    }
  },
}

</script>
