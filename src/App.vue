<template>
<div id="app">
  <div class="app-phone">
  <div class="phone-header">
    <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/1211695/vue_gram_logo_cp.png" />
  </div>
  <phone-body
    :step="step"
    :posts="posts"
    :filters="filters"
    :image="image"
    :selectedFilter="selectedFilter"
    v-model="caption"/>
  <div class="phone-footer">
    <div class="home-cta">
      <i class="fas fa-home fa-lg"></i>
    </div>
    <div class="upload-cta">
      <input type="file"
        name="file"
        id="file"
        class="inputfile"
        @change="uploadImage"/>
      <label for="file">
        <i class="far fa-plus-square fa-lg"></i>
      </label>
    </div>
  </div>
  </div>
  </div>
</template>

<script lang="ts">

import { Component, Vue } from 'vue-property-decorator';
import posts from './data/posts';
import filters from './data/filters';
import PhoneBody from './components/PhoneBody/PhoneBody.vue';
import EventBus from '@/event-bus';

@Component({
  components: {
  PhoneBody
  }})

export default class App extends Vue {
  posts : Array<{}> = [];
  filters : Array<{}> = [];
  step : number = 1;
  image : String = '';
  selectedFilter : String = '';
  caption : any = 1;

  constructor() {
    super();
    this.posts = posts;
    this.filters = filters;
  }

  uploadImage(evt : any) {
    const { files } = evt.target;
    if (!files.length) return;
    const reader = new FileReader();
    reader.readAsDataURL(files[0]);
    reader.onload = (evt2 : any) => {
      this.image = evt2.target.result;
      this.step = 2;
    };
    // To enable reuploading of same files in Chrome
    const file = document.querySelector('#file') || {};
    // file.value = '';
  }

  created() {
    EventBus.$on('filter-selected', (evt : any) => { this.selectedFilter = evt.filter; });
  }
}

</script>

<style lang="scss" src="./App.scss"></style>
