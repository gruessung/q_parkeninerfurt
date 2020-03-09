<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title>
          Parken in Erfurt
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="200"
      :breakpoint="400"

    >
      <q-scroll-area style="height: calc(100% - 150px); margin-top: 150px; border-right: 1px solid #ddd">
        <q-list padding>
          <q-item to="/" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="inbox"/>
            </q-item-section>

            <q-item-section>
              Parkhäuser
            </q-item-section>
          </q-item>

<!--
          <q-item to="/info" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="info"/>
            </q-item-section>

            <q-item-section>
              Über
            </q-item-section>
          </q-item>
-->
        </q-list>
      </q-scroll-area>

      <q-img class="absolute-top" src="https://img.gruessung.eu/?f=1583736753.png" style="height: 150px">
        <div class="absolute-bottom bg-transparent">
          <div class="text-weight-bold">Parken in Erfurt</div>
          <div>@gruessung</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container class="">
      <router-view></router-view>
    </q-page-container>
  </q-layout>
</template>

<script>
  export default {
    name: 'MainLayout',

    data() {
      return {
        leftDrawerOpen: false,
      }
    },
  }
</script>
