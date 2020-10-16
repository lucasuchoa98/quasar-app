<template>
  <q-layout view="lHh Lpr lFf">
    <q-header >
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />
      </q-toolbar>
    </q-header>

          <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-2"
    >
      <q-list>
        <q-item-label header>Uchôa APP</q-item-label>

        <q-expansion-item 
          expand-separator 
          icon="list"
          label="Áreas"
          caption="3 áreas existentes"
          default-opened
          >
          <q-item
          clickable tag="a" 
          href="#" 
          :header-inset-level="1">
          <q-item-section avatar>
          </q-item-section >
            <q-item-section>
            <q-item-label>Área 1</q-item-label>
          </q-item-section>
          </q-item> <q-item
          clickable tag="a" 
          href="#" 
          :header-inset-level="1">
          <q-item-section avatar>
          </q-item-section >
            <q-item-section>
            <q-item-label>Área 2</q-item-label>
          </q-item-section>
          </q-item> <q-item
          clickable tag="a" 
          href="#" 
          :header-inset-level="1">
          <q-item-section avatar>
          </q-item-section >
            <q-item-section>
            <q-item-label>Área 3</q-item-label>
          </q-item-section>
          </q-item> 


        </q-expansion-item>


        <q-item clickable tag="a" href="#" >
          <q-item-section avatar>
            <q-icon name="person" />
          </q-item-section >
            <q-item-section>
            <q-item-label>Clientes</q-item-label>
          </q-item-section>
        </q-item>
        <q-item clickable tag="a" href="#" >
          <q-item-section avatar>
            <q-icon name="logout" />
          </q-item-section >
            <q-item-section>
            <q-item-label>Sair</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>
    <q-page-container>
      <keep-alive>
      <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'
import  {date} from 'quasar'


export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false,
      loged: false,
    }
  },
  methods: {
    loginOrLogout () {
      return loged
    }
  }
}
</script>
