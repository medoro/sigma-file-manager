<!-- SPDX-License-Identifier: GPL-3.0-or-later
License: GNU GPLv3 or later. See the license file in the project root for more information.
Copyright © 2021 - present Aleksey Hoffman. All rights reserved.
-->

<script setup lang="ts">
import {Title} from '@/components/home/title';
import {Button} from '@/components/ui/button';
</script>

<template>
  <main class="home-page-content">
    <Title />
    <Button tooltip="Test tooltip prop">
      Project page
    </Button>
    <Button>
      Test
      <template #tooltip>
        Test tooltip slot content
      </template>
    </Button>
  </main>
</template>

<style>
.home-page-content {
  padding: 0 20px;
}
</style>
