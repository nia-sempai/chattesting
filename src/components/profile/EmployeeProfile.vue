<template>
  <div>
    <v-card>
      <v-card-title>{{ employee.fullName }}</v-card-title>
      <v-card-subtitle>{{ employee.position }}</v-card-subtitle>
      <v-img :src="employee.photoUrl"></v-img>
      <v-card-text>
        <v-list dense>
          <v-list-item v-for="achievement in achievements" :key="achievement.id">
            <v-icon :color="achievement.color">{{ achievement.icon }}</v-icon>
            <div>{{ achievement.title }}</div>
            <achievement-tooltip :achievement="achievement"></achievement-tooltip>
          </v-list-item>
        </v-list>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>

import AchievementTooltip from "@/components/profile/AchievementTooltip.vue";

export default {
  name: 'EmployeeProfile',
  components: {AchievementTooltip},
  props: {
    employee: { type: Object, required: true },
  },
  computed: {
    achievements() {
      return [
        {
          id: 1,
          title: "Награда за лучшую работу",
          icon: "mdi-trophy-variant-outline",
          color: "yellow darken-2",
          description: "Получено за лучшую работу в компании в этом месяце.",
        },
        {
          id: 2,
          title: "Награда за высокие результаты",
          icon: "mdi-chart-line-variant",
          color: "green darken-2",
          description: "Получено за высокие результаты в работе в этом месяце.",
        },
        {
          id: 3,
          title: "Награда за трудолюбие",
          icon: "mdi-hammer-screwdriver",
          color: "blue darken-2",
          description: "Получено за усердную работу в компании в этом месяце.",
        },
        {
          id: 4,
          title: "Награда за инновационность",
          icon: "mdi-lightbulb-on-outline",
          color: "purple darken-2",
          description: "Получено за вклад в развитие компании и предложение инновационных решений.",
        },
        {
          id: 5,
          title: "Награда за мастерство",
          icon: "mdi-hammer-wrench",
          color: "red darken-2",
          description: "Получено за высокую квалификацию и мастерство в работе.",
        }
      ]
    },
  },
}
</script>