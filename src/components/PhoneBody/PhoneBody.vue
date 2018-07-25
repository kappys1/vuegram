<template>
    <div class="phone-body">
    <div class="feed">
      <VuegramPost v-for="post in posts"
        :post="post"
        :key="posts.indexOf(post)">
      </VuegramPost>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import VuegramPost from '../VuegramPost/VuegramPost.vue';

@Component({
  components: {
     VuegramPost
  }
})
export default class PhoneBody extends Vue {
    @Prop() public posts!: Array<{}>;
    @Prop() public filters!: Array<{}>;
}
</script>

<style lang="scss" src="./PhoneBody.scss">
</style>

