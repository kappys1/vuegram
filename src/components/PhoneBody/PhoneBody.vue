<template>
    <div class="phone-body">
    <div class="feed" v-if="step === 1">
      <VuegramPost v-for="post in posts"
        :post="post"
        :key="posts.indexOf(post)">
      </VuegramPost>
    </div>
    <div v-if="step === 2 || step === 3">
      <div class="selected-image"
        :class="selectedFilter"
        :style="{ backgroundImage: 'url(' + image + ')' }">
      </div>
    </div>
    <div v-if="step === 2">
      <div class="filter-container">
        <FilterType v-for="filter in filters"
          :filter="filter"
          :image="image"
          :key="filters.indexOf(filter)" />
      </div>
    </div>
    <div v-if="step === 3">
      <div class="caption-container">
        <textarea class="caption-input"
          placeholder="Write a caption..."
          type="text"
          :value="value"
          @input="$emit('input', $event.target.value)">
        </textarea>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import VuegramPost from '../VuegramPost/VuegramPost.vue';
import FilterType from '../FilterType/FilterType.vue';

@Component({
  components: {
  VuegramPost,
  FilterType
  }
  })
export default class PhoneBody extends Vue {
    @Prop() public posts!: Array<{}>;
    @Prop() public filters!: Array<{}>;
    @Prop() public step!: Number;
    @Prop() public image!: String;
    @Prop() public selectedFilter!: String;
    @Prop() public value!: String;
}
</script>

<style lang="scss" src="./PhoneBody.scss"></style>

