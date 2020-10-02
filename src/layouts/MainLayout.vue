<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
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
      <div class="q-px-lg q-pt-l q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">{{todaysDate}}</div>
      </div>
      <q-img
        src="https://cdn.pixabay.com/photo/2020/08/23/14/55/castle-5511046_1280.jpg"
        class="header-image absolute-top" />
    </q-header>

     <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="180"
        :breakpoint="450"
      >
        <q-scroll-area style="height: calc(100% - 144px); margin-top: 144px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item
             to="/" 
             clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Todo
              </q-item-section>
            </q-item>

            <q-item 
              to="/help"
              exact
              clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Help
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="https://cdn.pixabay.com/photo/2020/08/23/14/55/castle-5511046_1280.jpg" style="height: 144px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="65px" class="q-mb-sm">
              <img src="https://id.gravatar.com/userimage/193757219/005eccff5be0ed3578b2d98ff5cd9c07.jpg">
            </q-avatar>
            <div class="text-weight-bold">Farris Permana</div>
            <div>@MasTolle</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'

export default {
  name: 'MainLayout',

  data () {
    return {
      leftDrawerOpen: false,
      
    }
  },
  computed: {
    todaysDate () {
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMM YYYY')
    }
  }
}
</script>

<style lang="scss">
  .header-image {
    height: 100%;
    z-index: -1;
    opacity: 0.5;
  }
</style>