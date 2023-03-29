<template>
  <v-app>
    <v-app-bar
        app
        color="primary"
        dark
    >
      <div class="d-flex align-center">
        <v-img
            alt="Vuetify Logo"
            class="shrink mr-2"
            contain
            src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
            transition="scale-transition"
            width="40"
        />

        <v-img
            alt="Vuetify Name"
            class="shrink mt-1 hidden-sm-and-down"
            contain
            min-width="100"
            src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
            width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
          href="https://github.com/vuetifyjs/vuetify/releases/latest"
          target="_blank"
          text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <employee-profile :employee="{
        fullName: 'Иванов Иван Иванович',
        position: 'Менеджер проекта',
        photoUrl: 'https://www.example.com/photo.jpg'}"
      />

      <achievements-list :achievements="achievements"/>
      
      <administrator-cabinet/>

    </v-main>
  </v-app>
</template>

<script>
import AdministratorCabinet from "@/components/administrator_cabinet/AdministratorCabinet.vue";
import EmployeeProfile from "@/components/profile/EmployeeProfile.vue";
import AchievementsList from "@/components/AchievementsList.vue";

export default {
  name: 'App',

  components: {
    AchievementsList,
    EmployeeProfile,
    AdministratorCabinet,
  },

  data: () => ({
    achievements: [
      {
        id: 1,
        name: 'Награда за вклад в развитие проекта',
        description: 'Был отмечен за внесение значительного вклада в развитие проекта',
        icon: 'mdi-trophy',
        date: '2021-10-10',
      },
      {
        id: 2,
        name: 'Победитель хакатона',
        description: 'Стал победителем хакатона по созданию приложения для сокращения времени, затраченного на выполнение задач',
        icon: 'mdi-crown',
        date: '2021-08-15',
      },
      {
        id: 3,
        name: 'Лучший сотрудник месяца',
        description: 'Стал лучшим сотрудником месяца по результатам выполнения KPI в отделе продаж',
        icon: 'mdi-medal',
        date: '2022-02-01',
      },
      {
        id: 4,
        name: 'Номинация на премию в области IT',
        description: 'Стал номинантом на премию в области IT за разработку инновационной платформы',
        icon: 'mdi-trophy-award',
        date: '2022-01-20',
      },
      {
        id: 5,
        name: 'Лучший сотрудник года',
        description: 'Стал лучшим сотрудником года в компании по итогам голосования сотрудников',
        icon: 'mdi-crown',
        date: '2021-12-31',
      },
    ],
    //
  }),
};
</script>
