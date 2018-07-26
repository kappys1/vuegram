<template>
  <div class="filter-type">
    <p>{{filter.name}}</p>
    <div class="img"
      :class="filter.name"
      :style="{ backgroundImage: 'url(' + image + ')' }"
      @click="selectFilter">
    </div>
  </div>
</template>

<script lang="ts">
import EventBus from '../../event-bus';
import { Component, Prop, Vue } from 'vue-property-decorator';
import { IPost } from '@/data/posts';
import { IFilter } from '@/data/filters';

@Component
export default class FilterType extends Vue {
    @Prop() public filter!: IFilter;
    @Prop() public image!: String;

    selectFilter() {
      EventBus.$emit('filter-selected', { filter: this.filter.name });
    }
}
</script>

<style lang="scss" src="./FilterType.scss"></style>

