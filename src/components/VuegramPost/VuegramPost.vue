<template>
  <div class="vuegram-post">
    <div class="header level">
        <div class="level-left">
          <figure class="image is-32x32">
            <img :src="post.userImage" />
          </figure>
          <span class="username">{{post.username}}</span>
        </div>
    </div>
    <div class="image-container"
      :class="post.filter"
      :style="{ backgroundImage: 'url(' + post.postImage + ')' }"
      v-on:dblclick="like">
    </div>
    <div class="content">
      <div class="heart">
        <i class="far fa-heart fa-lg"
           :class="{'fas': this.post.hasBeenLiked}"
           @click="like">
        </i>
      </div>
      <p class="likes">{{post.likes}} likes</p>
      <p class="caption"><span>{{post.username}}</span> {{post.caption}}</p>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import { IPost } from '@/data/posts';

@Component
export default class VuegramPost extends Vue {
    @Prop() public post!: IPost;

    like() {
      console.log("click");
      if (this.post.hasBeenLiked) {
        this.post.likes = this.post.likes - 1;
      } else {
        this.post.likes = this.post.likes + 1;
      }
      this.post.hasBeenLiked = !this.post.hasBeenLiked;
    }
}
</script>

<style lang="scss" src="./VuegramPost.scss">
</style>

