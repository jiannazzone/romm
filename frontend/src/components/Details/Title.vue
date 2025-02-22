<script setup lang="ts">
import { useDisplay } from "vuetify";
import PlatformIcon from "@/components/Platform/PlatformIcon.vue";
import { regionToEmoji, languageToEmoji } from "@/utils";
import type { Rom } from "@/stores/roms";

defineProps<{ rom: Rom }>();
const { mdAndUp } = useDisplay();
</script>
<template>
  <v-row class="text-white text-shadow" :class="{ 'mr-16': mdAndUp }" no-gutters>
    <v-col
      cols="12"
      class="text-h5 font-weight-bold px-1"
    >
      <span>{{ rom.name }}</span>
    </v-col>
    <v-col cols="12">
      <v-chip
        class="font-italic px-3 my-2"
        :to="`/platform/${rom.platform_slug}`"
      >
        {{ rom.platform_name || rom.platform_slug }}
        <v-avatar :rounded="0" size="40" class="ml-2 pa-1">
          <platform-icon :platform="rom.platform_slug"></platform-icon>
        </v-avatar>
      </v-chip>
      <v-chip
        class="ml-2 my-2"
        v-if="rom.regions.filter((i: string) => i).length > 0"
        :title="`Regions: ${rom.regions.join(', ')}`"
      >
        <span class="px-1" v-for="region in rom.regions">{{
          regionToEmoji(region)
        }}</span>
      </v-chip>
      <v-chip
        class="ml-2 my-2"
        v-if="rom.languages.filter((i: string) => i).length > 0"
        :title="`Languages: ${rom.languages.join(', ')}`"
      >
        <span class="px-1" v-for="language in rom.languages">{{
          languageToEmoji(language)
        }}</span>
      </v-chip>
      <v-chip v-show="rom.revision" class="ml-2 my-2"
        >Revision {{ rom.revision }}
      </v-chip>
    </v-col>
  </v-row>
</template>

<style scoped>
.text-shadow {
  text-shadow: 1px 1px 3px #000000, 0 0 3px #000000;
}
</style>
