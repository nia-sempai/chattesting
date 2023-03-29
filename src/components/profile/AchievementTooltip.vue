<template>
  <v-tooltip right>
    <template v-slot:activator="{ on }">
      <v-icon v-on="on" color="grey lighten-1">mdi-information-outline</v-icon>
    </template>
    <div>{{ achievement.title }}</div>
  </v-tooltip>
</template>

<script>
export default {
  name: 'AchievementTooltip',
  props: {
    achievement: { type: Object, required: true },
  },
}
</script>