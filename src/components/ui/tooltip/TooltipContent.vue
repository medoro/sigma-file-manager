<!-- SPDX-License-Identifier: GPL-3.0-or-later
License: GNU GPLv3 or later. See the license file in the project root for more information.
Copyright © 2021 - present Aleksey Hoffman. All rights reserved.
-->

<script setup lang="ts">
import {TooltipContent, TooltipPortal, useForwardPropsEmits} from 'radix-vue';
import {type HTMLAttributes} from 'vue';
import type {TooltipContentEmits, TooltipContentProps} from 'radix-vue';

const props = withDefaults(defineProps<TooltipContentProps & { class?: HTMLAttributes['class'] }>(), {
  sideOffset: 4,
  side: 'bottom'
});
const emit = defineEmits<TooltipContentEmits>();

const forwarded = useForwardPropsEmits(props, emit);
</script>

<template>
  <TooltipPortal>
    <TooltipContent
      v-bind="{ ...forwarded, ...$attrs }"
      :class="['ui-tooltip-content', props.class]"
      :side="side"
    >
      <slot />
    </TooltipContent>
  </TooltipPortal>
</template>

<style>
.ui-tooltip-content {
  z-index: 5;
  min-height: 24px;
  padding: 6px 12px;
  border-radius: var(--rounded);
  animation-duration: 0.6s;
  animation-timing-function: cubic-bezier(0.16, 1, 0.3, 1);
  backdrop-filter: blur(4px);
  background: white;
  background-color: rgb(var(--light-value) / 30%);
  color: black;
  cursor: default;
  transition: all 0.5s ease;
}

.ui-tooltip-content[data-side="top"] {
  animation-name: slide-up;
}

.ui-tooltip-content[data-side="bottom"] {
  animation-name: slide-down;
}

@keyframes slide-down {
  from {
    opacity: 0;
    transform: translateY(-20px) scale(0.5);
  }

  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes slide-up {
  from {
    opacity: 0;
    transform: translateY(20px) scale(0.5);
  }

  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}
</style>