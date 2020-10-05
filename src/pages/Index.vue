<template>
  <q-page>
    <div class="q-gutter-md" style="max-width: 300px">
      <q-list v-for="(pessoa,index) in pessoas" v-bind:key="index" bordered separator v-show="true"  style="margin: 0px 16px">
        <transition appear enter-active-class="animated fadeIn" leave-active-class="animated fadeOut">
          <q-item clickable>
            <q-item-section> Nome: {{ pessoa.name }} </q-item-section>
            <q-item-section> Idade: {{ pessoa.age }} </q-item-section>
          </q-item>
        </transition>
      </q-list>
      
      <q-form
        @submit="addPessoa"
        @reset="onReset"
        class="q-gutter-md"
      >
      <q-input
        filled
        v-model="nome"
        label="Your name *"
        hint="Name and surname"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />

      <q-input
        filled
        type="number"
        v-model="idade"
        label="Your age *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your age',
          val => val > 0 && val < 100 || 'Please type a real age'
        ]"
      />

      <q-toggle v-model="accept" label="I accept the license and terms" />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  

    </div>
  </q-page>
</template>

<script>
import { openURL, Quasar, QSelect } from 'quasar';
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

const livro_list = ['Livro1', 'Livro2']


export default {
  data () {
    return {
      pessoas: [
        {
          name: 'Lucas',
          age: 21,
        },{
          name:'Robertinho',
          age: 22
        }
      ],
      name: null,
      age: null,

      accept: false
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
    },
    onSubmit () {
      if (this.accept !== true) {
        this.$q.notify({
          color: 'red-5',
          textColor: 'white',
          icon: 'warning',
          message: 'You need to accept the license and terms first'
        })


      }
      else {
        this.$q.notify({
          color: 'green-4',
          textColor: 'white',
          icon: 'cloud_done',
          message: 'Submitted'
        })
      }

    },
    onReset () {
      this.name = null
      this.age = null
      this.accept = false
    },
    addPessoa () {
          this.pessoas.push({
          name: this.nome,
          age: this.idade
        })
      }
  }
}

</script>
