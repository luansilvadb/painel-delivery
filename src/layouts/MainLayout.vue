<template>
  <q-layout view="lhr lpr lfr">
    <q-drawer
      style="overflow-x: hidden"
      show-if-above
      v-model="drawer"
      side="left"
      :width="200"
      :mini="!drawer || miniState"
      @click.capture="drawerClick"
    >
      <div class="logo-header">
        <q-img
          class="logo-image"
          :src="
            miniState
              ? 'https://svgshare.com/i/12Bf.svg'
              : 'https://svgshare.com/i/12E9.svg'
          "
        />
      </div>

      <q-list style="opacity: 90%">
        <q-item v-for="item in menuItems" :key="item.label" clickable v-ripple>
          <q-item-section avatar>
            <q-icon :name="item.icon" />
          </q-item-section>
          <q-item-section>{{ item.label }}</q-item-section>
        </q-item>
      </q-list>

      <div class="drawer-footer">
        <q-btn v-if="miniState" dense flat round @click="miniState = false">
          <i class="material-icons">arrow_back</i>
        </q-btn>
        <q-btn v-else dense flat round @click="miniState = true">
          <i class="material-icons">arrow_forward</i>
        </q-btn>
      </div>
    </q-drawer>

    <q-header reveal class="bg-white text-white">
      <q-toolbar style="padding: 10px 0px 30px 20px">
        <q-input
          rounded
          type="search"
          style="height: 20px; width: 500px"
          outlined
          placeholder="Search by Store ID, E-mail, Keyword"
          dense
        >
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </q-toolbar>
    </q-header>

    <q-page-container style="background-color: #f5f5f5">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue';

const miniState = ref(false);
const drawer = ref(false);

const drawerClick = (e) => {
  if (miniState.value) {
    miniState.value = false;
    e.stopPropagation();
  }
};

const menuItems = [
  { label: 'Dashboard', icon: 'speed' },
  { label: 'Orders', icon: 'restaurant_menu' },
  { label: 'Users', icon: 'people' },
  { label: 'Products', icon: 'shopping_cart' },
  { label: 'Stores', icon: 'store' },
  { label: 'Categories', icon: 'category' },
  { label: 'Couriers', icon: 'local_shipping' },
  { label: 'Reviews', icon: 'try' },
  { label: 'Logout', icon: 'logout' },
];
</script>

<style scoped>
.logo-header {
  padding: 0px 0px 0px 9px;
  height: 64px;
  display: flex;
  align-items: center;
}

.drawer-footer {
  position: fixed;
  bottom: 0;
  z-index: 1;
  height: 48px;
  color: #000000;
  line-height: 48px;
  text-align: center;
  width: 100%;
}
</style>
