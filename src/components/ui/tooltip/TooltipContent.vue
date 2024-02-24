<!-- SPDX-License-Identifier: GPL-3.0-or-later
License: GNU GPLv3 or later. See the license file in the project root for more information.
Copyright © 2021 - present Aleksey Hoffman. All rights reserved.
-->

<script setup lang="ts">
import {TooltipContent, TooltipPortal, useForwardPropsEmits} from 'radix-vue';
import {type HTMLAttributes} from 'vue';
import type {TooltipContentEmits, TooltipContentProps} from 'radix-vue';

const props = withDefaults(defineProps<TooltipContentProps & { class?: HTMLAttributes['class'] }>(), {
  sideOffset: 8,
  side: 'bottom'
});
const emit = defineEmits<TooltipContentEmits>();

const forwarded = useForwardPropsEmits(props, emit);
</script>

<template>
  <TooltipPortal force-mount>
    <Transition :name="`tooltip-${side}`">
      <TooltipContent
        v-bind="{ ...forwarded, ...$attrs }"
        :class="['ui-tooltip-content', props.class]"
        :side="side"
      >
        <slot />
      </TooltipContent>
    </Transition>
  </TooltipPortal>
</template>

<style>
.ui-tooltip-content {
  z-index: 5;
  min-height: 24px;
  padding: 8px 16px;
  border-radius: var(--rounded);
  backdrop-filter: blur(4px);
  background-color: hsl(from hsl(var(--background)) h s calc(l + 2%) / 80%);
  box-shadow: 0 2px 48px hsl(var(--dark) / 24%);
  color: var(--grey-500);
  cursor: default;
}

.tooltip-bottom-leave-active {
  transition:
    opacity 0.1s ease,
    translate 0.1s ease;
  }

.tooltip-bottom-enter-active {
  transition:
    opacity 0.1s ease,
    translate 0.1s ease;
}

.tooltip-bottom-enter-from,
.tooltip-bottom-leave-to {
  opacity: 0;
  translate: 0 -20px;
}
</style>