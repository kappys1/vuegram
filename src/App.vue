<template>
<div id="app">
  <div class="app-phone">
  <div class="phone-header">
    <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/1211695/vue_gram_logo_cp.png" />
  </div>
  <phone-body />
  <div class="phone-footer">
  <div class="home-cta">
    <i class="fas fa-home fa-lg"></i>
  </div>
  <div class="upload-cta">
    <i class="far fa-plus-square fa-lg"></i>
  </div>
  </div>
  </div>
  </div>
</template>

<script lang="ts">

import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld/HelloWorld.vue';
import PhoneBody from './components/PhoneBody/PhoneBody.vue';

@Component({
  components: {
  HelloWorld,
  PhoneBody
  }})

export default class App extends Vue {}

</script>

<style lang="scss" src="./App.scss"></style>
