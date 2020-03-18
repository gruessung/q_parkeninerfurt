<template>
  <q-layout view="lHh Lpr lFf">





    <q-header elevated>

      <q-bar class="q-electron-drag" v-if="$q.platform.is.electron">
        <q-icon name="car" />
        <div>Parken in Erfurt</div>

        <q-space />

        <q-btn dense flat icon="minimize" @click="minimize" />
        <q-btn dense flat icon="crop_square" @click="maximize" />
        <q-btn dense flat icon="close" @click="closeApp" />
      </q-bar>
<!--
      <div class="q-pa-sm q-pl-md row items-center">
        <div class="cursor-pointer non-selectable">
          File
          <q-menu>
            <q-list dense style="min-width: 100px">
              <q-item clickable v-close-popup>
                <q-item-section>Open...</q-item-section>
              </q-item>
              <q-item clickable v-close-popup>
                <q-item-section>New</q-item-section>
              </q-item>

              <q-separator />

              <q-item clickable>
                <q-item-section>Preferences</q-item-section>
                <q-item-section side>
                  <q-icon name="keyboard_arrow_right" />
                </q-item-section>

                <q-menu anchor="top right" self="top left">
                  <q-list>
                    <q-item
                      v-for="n in 3"
                      :key="n"
                      dense
                      clickable
                    >
                      <q-item-section>Submenu Label</q-item-section>
                      <q-item-section side>
                        <q-icon name="keyboard_arrow_right" />
                      </q-item-section>
                      <q-menu auto-close anchor="top right" self="top left">
                        <q-list>
                          <q-item
                            v-for="n in 3"
                            :key="n"
                            dense
                            clickable
                          >
                            <q-item-section>3rd level Label</q-item-section>
                          </q-item>
                        </q-list>
                      </q-menu>
                    </q-item>
                  </q-list>
                </q-menu>
              </q-item>

              <q-separator />

              <q-item clickable v-close-popup @click="closeApp">
                <q-item-section>Quit</q-item-section>
              </q-item>
            </q-list>
          </q-menu>
        </div>

        <div class="q-ml-md cursor-pointer non-selectable">
          Edit
          <q-menu auto-close>
            <q-list dense style="min-width: 100px">
              <q-item clickable>
                <q-item-section>Cut</q-item-section>
              </q-item>
              <q-item clickable>
                <q-item-section>Copy</q-item-section>
              </q-item>
              <q-item clickable>
                <q-item-section>Paste</q-item-section>
              </q-item>
              <q-separator />
              <q-item clickable>
                <q-item-section>Select All</q-item-section>
              </q-item>
            </q-list>
          </q-menu>
        </div>
      </div>-->

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
      elevated
      behavior="mobile"
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

          <q-item to="/info" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="info"/>
            </q-item-section>

            <q-item-section>
              Über
            </q-item-section>
          </q-item>

          <q-item v-if="$q.platform.is.desktop" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="business"/>
            </q-item-section>

            <q-item-section>
              <a href="https://impressum.gruessung.eu/88ed3a49d06b633391c91029be7f0659.html" target="_blank" class="text-black" style="text-decoration: none;">Impressum</a>
            </q-item-section>
          </q-item>
          <q-item v-if="$q.platform.is.desktop" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="apps"/>
            </q-item-section>

            <q-item-section>
              <a href="https://impressum.gruessung.eu/88ed3a49d06b633391c91029be7f0659/1.html" target="_blank" class="text-black" style="text-decoration: none;">Datenschutz</a>
            </q-item-section>
          </q-item>

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

    methods: {
      minimize () {
        if (process.env.MODE === 'electron') {
          this.$q.electron.remote.BrowserWindow.getFocusedWindow().minimize()
        }
      },

      maximize () {
        if (process.env.MODE === 'electron') {
          const win = this.$q.electron.remote.BrowserWindow.getFocusedWindow()

          if (win.isMaximized()) {
            win.unmaximize()
          }
          else {
            win.maximize()
          }
        }
      },

      closeApp () {
        if (process.env.MODE === 'electron') {
          this.$q.electron.remote.BrowserWindow.getFocusedWindow().close()
        }
      }
    }
  }
</script>
