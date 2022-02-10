<template>
  <q-layout view="hHh lpR fFf">

    <q-header bordered class="bg-primary text-white">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toogleDrawer" />

        <q-toolbar-title>
          <!-- <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
          </q-avatar> -->
          理財幫手
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <!-- <q-drawer v-model="leftDrawerOpen" side="left" overlay bordered>
    </q-drawer> -->
      <q-drawer
        v-model="drawer"
        show-if-above

        :mini="!drawer || miniState"
        @click.capture.stop="miniState = !miniState "

        :width="200"
        :breakpoint="500"
        bordered
        class="bg-grey-3"
      >
        <template v-slot:mini>
          <q-scroll-area class="fit mini-slot cursor-pointer">
            <div class="q-py-lg">
              <div class="column items-center">
                <q-icon name="inbox" color="blue" class="mini-icon" />
                <q-icon name="star" color="orange" class="mini-icon" />
                <q-icon name="send" color="purple" class="mini-icon" />
                <q-icon name="drafts" color="teal" class="mini-icon" />
              </div>
            </div>
          </q-scroll-area>
        </template>

        <q-scroll-area class="fit">
          <q-list padding>
            <q-item clickable v-ripple>
              <q-item-section>
                Inbox
              </q-item-section>
            </q-item>

            <q-item active clickable v-ripple>
              <q-item-section>
                Star
              </q-item-section>
            </q-item>

            <q-item clickable v-ripple>
              <q-item-section>
                Send
              </q-item-section>
            </q-item>

            <q-item clickable v-ripple>
              <q-item-section>
                Drafts
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>

        <!--
          in this case, we use a button (can be anything)
          so that user can switch back
          to mini-mode
        -->
        <div class="q-mini-drawer-hide absolute" style="top: 15px; right: -17px">
          <q-btn
            dense
            round
            unelevated
            color="accent"
            icon="chevron_left"
            @click="miniState = true"
          />
        </div>
      </q-drawer>

    <q-page-container>
      <div>drawer: {{drawer}}</div>
      <div>miniState: {{miniState}}</div>
      <div>menu: {{menus}}</div>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import menus from './objects/menus'

const drawer = ref(false)
const miniState  = ref(true)

function toogleDrawer(){
  drawer.value = !drawer.value
}
function drawerClick(e: Event) {
   if (miniState.value) {
          miniState.value = false
          e.stopPropagation()
        }
}
</script>
<style lang="scss" scoped>
.mini-slot
{
  transition: background-color .28s;
  &:hover {
    background-color: rgba(0, 0, 0, .04)
  }
}

.mini-icon{
  font-size: 1.718em;
  & + & {
    margin-top: 18px
  };
}
</style>