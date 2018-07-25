<template>
    <div class="phone-body">
        This is the Phone Body
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import VuegramPost from '../VuegramPost/VuegramPost.vue';

@Component
export default class PhoneBody extends Vue {
    @Prop() public posts!: Array<{}>;
    @Prop() public filters!: Array<{}>;
}
</script>

<style lang="scss" src="./PhoneBody.scss">
</style>

