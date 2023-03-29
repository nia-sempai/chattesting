<template>
  <div>
    <v-card>
      <v-card-title>
        <div class="headline">Достижения</div>
        <v-menu offset-y>
          <template v-slot:activator="{ on, attrs }">
            <v-btn
                icon
                v-bind="attrs"
                v-on="on"
            >
              <v-icon>mdi-filter-variant</v-icon>
            </v-btn>
          </template>
          <v-list>
            <v-list-item @click="sortByDate">
              <v-list-item-title>Сортировать по дате</v-list-item-title>
            </v-list-item>
            <v-list-item @click="sortByName">
              <v-list-item-title>Сортировать по имени</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-card-title>
      <v-list>
        <v-list-item
            v-for="achievement in sortedAchievements"
            :key="achievement.id"
        >
          <v-list-item-avatar>
            <v-icon>{{ achievement.icon }}</v-icon>
          </v-list-item-avatar>
          <v-list-item-content>
            <v-list-item-title class="headline font-weight-bold">
              {{ achievement.name }}
            </v-list-item-title>
            <v-list-item-subtitle>{{ achievement.description }}</v-list-item-subtitle>
            <v-list-item-subtitle>
              {{ formatDate(achievement.date) }}
            </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {
    achievements: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      sortBy: "date",
      sortDesc: true
    };
  },
  computed: {
    sortedAchievements() {
      const sorted = [...this.achievements].sort((a, b) => {
        if (this.sortBy === "name") {
          if (a.name < b.name) return this.sortDesc ? 1 : -1;
          if (a.name > b.name) return this.sortDesc ? -1 : 1;
        } else {
          return this.sortDesc
              ? new Date(b.date) - new Date(a.date)
              : new Date(a.date) - new Date(b.date);
        }
      });
      return sorted;
    }
  },
  methods: {
    formatDate(date) {
      const options = { year: "numeric", month: "long", day: "numeric" };
      return new Date(date).toLocaleDateString("ru-RU", options);
    },
    sortByDate() {
      this.sortBy = "date";
      this.sortDesc = !this.sortDesc;
    },
    sortByName() {
      this.sortBy = "name";
      this.sortDesc = !this.sortDesc;
    }
  }
};
</script>
