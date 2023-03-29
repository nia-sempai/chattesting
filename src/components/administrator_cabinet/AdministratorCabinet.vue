<template>
  <div>
    <v-container>
      <v-row>
        <v-col cols="6">
          <v-card>
            <v-card-title>Список сотрудников</v-card-title>
            <v-card-text>
              <v-list dense>
                <v-list-item v-for="employee in employees" :key="employee.id">
                  <v-list-item-action>
                    <v-checkbox v-model="employee.checked"></v-checkbox>
                  </v-list-item-action>
                  <v-list-item-content>{{ employee.name }}</v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card-text>
          </v-card>
        </v-col>
        <v-col cols="6">
          <v-card>
            <v-card-title>Список выданных достижений</v-card-title>
            <v-card-text>
              <v-list dense>
                <v-list-item v-for="achievement in achievements" :key="achievement.id">
                  <v-list-item-content>{{ achievement.name }}</v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-card>
            <v-card-title>Добавить новое достижение</v-card-title>
            <v-card-text>
              <v-form ref="form" v-model="valid">
                <v-text-field label="Наименование достижения" v-model="name" :rules="nameRules"></v-text-field>
                <v-text-field label="Описание достижения" v-model="description" :rules="descriptionRules"></v-text-field>
                <v-file-input label="Иконка достижения" v-model="icon" :rules="iconRules"></v-file-input>
              </v-form>
            </v-card-text>
            <v-card-actions>
              <v-btn color="primary" @click="saveAchievement" :disabled="!valid">Сохранить достижение</v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'AdministratorCabinet',
  data() {
    return {
      employees: [
        { id: 1, name: 'Иванов Иван', checked: false },
        { id: 2, name: 'Петров Петр', checked: false },
        { id: 3, name: 'Сидоров Сидор', checked: false }
      ],
      achievements: [
        { id: 1, name: 'Награда за лучшую работу', icon: '', description: '' },
        { id: 2, name: 'Награда за высокие результаты', icon: '', description: '' }
      ],
      valid: false,
      name: '',
      nameRules: [
        value => !!value || 'Наименование достижения обязательно для заполнения',
        value => (value && value.length <= 50) || 'Наименование достижения не должно превышать 50 символов'
      ],
      description: '',
      descriptionRules: [
        value => !!value || 'Описание достижения обязательно для заполнения',
        value => (value && value.length <= 250) || 'Описание достижения не должно превышать 250 символов'
      ],
      icon: null,
      iconRules: [
        value => !!value || 'Иконка достижения обязательна для загрузки',
        value => value && value.size < 1000000 || 'Размер файла должен быть менее 1Мб',
        value => value && ['image/jpeg', 'image/png', 'image/gif'].includes(value.type) || 'Допустимые форматы: jpeg, png, gif'
      ]
    }
  },
  methods: {
    saveAchievement() {
      const newAchievement = {
        id: this.achievements.length + 1,
        name: this.name,
        description: this.description,
        icon: URL.createObjectURL(this.icon)
      }
      this.achievements.push(newAchievement)
      this.resetForm()
    },
    resetForm() {
      this.$refs.form.reset()
      this.icon = null
      this.valid = false
      this.name = ''
      this.description = ''
    }
  }
}
</script>
