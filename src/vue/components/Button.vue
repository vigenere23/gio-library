<template>
  <GioSmartLink
    class="gio-button"
    :class="{
      dark,
      'no-margin-left': noMarginLeft,
      'no-margin-right': noMarginRight,
      ...sizeClass
    }"
    :href="href"
    @click="$emit('click')"
  >
    <GioText :dark="dark" type="primary" class="gio-button__content">
      <slot></slot>
    </GioText>
  </GioSmartLink>
</template>

<script lang="ts">
import Vue from 'vue'
import { Darkable } from '@/lib/mixins/darkable'
import { mixins } from 'vue-class-component'
import { Component, Prop } from 'vue-property-decorator'
import GioText from '@/vue/components/typography/Text.vue'
import GioSmartLink from '@/vue/components/SmartLink.vue'

type Size = 'small' | 'medium'

const Props = Vue.extend({
  props: {
    href: { type: String, required: false },
    noMarginLeft: { type: Boolean, default: false },
    noMarginRight: { type: Boolean, default: false }
  }
})

@Component({
  name: 'GioButton',
  components: { GioText, GioSmartLink }
})
export default class GioButton extends mixins(Props, Darkable) {
  @Prop({ type: String, default: 'medium' }) size!: Size

  get sizeClass(): { [key: string]: boolean } {
    return {
      [this.size]: true
    }
  }
}
</script>

<style lang="scss">
@import '~@/lib/styles/colors';
@import '~@/lib/styles/transitions';
@import '~@/lib/styles/sizes';

.gio-button {
  display: flex;
  align-items: center;
  width: fit-content;
  background-color: $accent-light;
  color: $primary-text-dark;
  cursor: pointer;
  @include transition(base, out, color, background-color);

  &.medium {
    height: 9rem;
    padding: 0 3rem;
    border-radius: $border-radius-medium;
  }

  &.small {
    height: 8rem;
    padding: 0 2.5rem;
    border-radius: $border-radius-medium;

    .button-content > * {
      font-size: 0.9em;
    }
  }

  &:not(.no-margin-left) {
    margin-left: 2rem;
  }

  &:not(.no-margin-right) {
    margin-right: 2rem;
  }

  &:hover,
  &:active,
  &:focus {
    @include transition(base, in, color, background-color);
  }

  &:active,
  &:focus {
    background-color: $focus-light;
  }

  &:hover {
    background-color: $hover-light;
  }

  &.dark {
    background-color: $accent-dark;
    color: $primary-text-light;

    &:active,
    &:focus {
      background-color: $focus-dark;
    }

    &:hover {
      background-color: $hover-dark;
    }
  }

  > * {
    flex: 0 0 auto;
  }

  &__content {
    text-transform: uppercase;

    > :not(:first-child) {
      margin-left: 2rem;
    }

    > * {
      vertical-align: middle;
    }
  }
}
</style>
