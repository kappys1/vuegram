<template>
<div id='app'>
  <div class='app-phone'>
  <div class='phone-header'>
    <img src='https://s3-us-west-2.amazonaws.com/s.cdpn.io/1211695/vue_gram_logo_cp.png' />
    <a class='cancel-cta'
        v-if='step === 2 || step === 3'
        @click='goToHome'>
        Cancel
    </a>
    <a class='next-cta'
      v-if='step === 2'
      @click='step++'>
      Next
    </a>
    <a class='next-cta'
      v-if='step === 3'
      @click='sharePost'>
      Share
    </a>
  </div>
  <phone-body
    :step='step'
    :posts='posts'
    :filters='filters'
    :image='image'
    :selectedFilter='selectedFilter'
    v-model='caption'/>
  <div class='phone-footer'>
    <div class='home-cta' @click='goToHome'>
      <i class='fas fa-home fa-lg'></i>
    </div>
    <div class='upload-cta'>
      <input type='file'
        name='file'
        id='file'
        class='inputfile'
        :disabled='step !== 1'
        @change='uploadImage'/>
      <label for='file'>
        <i class='far fa-plus-square fa-lg'></i>
      </label>
    </div>
  </div>
  </div>
  </div>
</template>

<script lang='ts'>

import { Component, Vue } from 'vue-property-decorator';
import posts from './data/posts';
import filters from './data/filters';
import PhoneBody from './components/PhoneBody/PhoneBody.vue';
import EventBus from '@/event-bus';
import VueDragscroll from 'vue-dragscroll';

Vue.use(VueDragscroll);

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
    file.value = '';
  }

  created() {
    EventBus.$on('filter-selected', (evt : any) => { this.selectedFilter = evt.filter; });
  }
  goToHome() {
    this.image = '';
    this.selectedFilter = '';
    this.caption = '';
    this.step = 1;
  }
  sharePost() {
    const post = {
      username: 'fullstack_vue',
      userImage: 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/1211695/vue_lg_bg.png',
      postImage: this.image,
      likes: 0,
      caption: this.caption,
      filter: this.selectedFilter,
    };
    console.log(post);
    this.posts.unshift(post);
    this.goToHome();
  }
}

</script>

<style lang='scss' src='./App.scss'></style>
