<!-- SPDX-License-Identifier: GPL-3.0-or-later
License: GNU GPLv3 or later. See the license file in the project root for more information.
Copyright © 2021 - present Aleksey Hoffman. All rights reserved.
-->

<script setup lang="ts">
import {Primitive} from 'radix-vue';
import {computed, useSlots} from 'vue';
import {
  Tooltip,
  TooltipContent,
  TooltipProvider,
  TooltipTrigger
} from '@/components/ui/tooltip';


interface Props {
  type?: 'button' | 'icon';
  variant?: 'tonal';
  tooltip?: string;
  tooltipShortcuts?: Array<{ value: string; description: string }>;
  disabled?: boolean;
  size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
}

interface Emits {
  (event: 'click'): void;
}

const props = withDefaults(defineProps<Props>(), {
  type: 'button',
  variant: 'tonal',
  tooltip: '',
  tooltipShortcuts: () => [],
  disabled: false,
  size: 'sm'
});

const emit = defineEmits<Emits>();

const slots = useSlots();

const classMods = computed(() => ({
  'ui-button--tonal': props.variant === 'tonal'
}));

const isTooltipProvided = computed(() => (props.tooltip && props.tooltip.length !== 0) || Boolean(slots.tooltip));
</script>

<template>
  <TooltipProvider>
    <Tooltip>
      <TooltipTrigger as-child>
        <span tabindex="0">
          <Primitive
            class="ui-button"
            :class="classMods"
            :disabled="disabled"
            as="button"
            @click="emit('click')"
          >
            <slot />
          </Primitive>
        </span>
      </TooltipTrigger>
      <TooltipContent v-if="isTooltipProvided">
        <div v-if="props.tooltip">
          {{ props.tooltip }}
        </div>
        <slot
          v-if="slots.tooltip"
          name="tooltip"
        />
      </TooltipContent>
    </Tooltip>
  </TooltipProvider>
</template>

<style>
.ui-button {
  display: inline-flex;
  height: 28px;
  align-items: center;
  justify-content: center;
  padding: 0 12px;
  border-radius: var(--rounded-sm);
  cursor: pointer;
  font-size: 12px;
  font-weight: 500;
  outline: 2px solid;
  outline-color: rgb(var(--light-value) / 0%);
  outline-offset: 2px;
  text-transform: uppercase;
  transition: all 0.3s ease;
  user-select: none;
  white-space: nowrap;
}

.ui-button:focus-visible {
  outline-color: rgb(var(--light-value) / 100%);
}

.ui-button:disabled {
  opacity: 0.5;
  pointer-events: none;
}

.ui-button--tonal {
  background-color: rgb(var(--light-value) / 5%);
  color: rgb(var(--light-value) / 50%);
}
</style>