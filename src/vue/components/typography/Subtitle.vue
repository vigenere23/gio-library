<template>
  <div class="gio-subtitle" :class="{ dark, centered, ...noMarginClass }">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component } from 'vue-property-decorator'
import { Darkable } from '@/lib/mixins/darkable'
import { Centerable } from '@/lib/mixins/centerable'
import { NoMarginable } from '@/lib/mixins/no-marginable'
import { mixins } from 'vue-class-component'

@Component({
  name: 'GioSubtitle'
})
export default class GioSubtitle extends mixins(
  Darkable,
  Centerable,
  NoMarginable
) {}
</script>

<style lang="scss">
@import '~@/lib/styles/fonts';
@import '~@/lib/styles/colors';
@import '~@/lib/styles/sizes';

.gio-subtitle {
  font-family: $special-font;
  font-size: 5.5rem;
  font-weight: 700;
  color: $tertiary-text-dark;

  &:not(.no-margin) {
    @include text-margin;
  }

  &.centered {
    text-align: center;
  }

  &.dark {
    color: $tertiary-text-light;
  }
}
</style>
