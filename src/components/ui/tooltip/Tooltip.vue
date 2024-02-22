<!-- SPDX-License-Identifier: GPL-3.0-or-later
License: GNU GPLv3 or later. See the license file in the project root for more information.
Copyright © 2021 - present Aleksey Hoffman. All rights reserved.
-->

<script setup lang="ts">
import {TooltipRoot, useForwardPropsEmits} from 'radix-vue';
import type {TooltipRootEmits, TooltipRootProps} from 'radix-vue';

const props = defineProps<TooltipRootProps>();
const emits = defineEmits<TooltipRootEmits>();

const forwarded = useForwardPropsEmits(props, emits);
</script>

<template>
  <TooltipRoot
    v-bind="forwarded"
    :delay-duration="0"
  >
    <slot />
  </TooltipRoot>
</template>
