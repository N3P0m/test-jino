<template>

  <div class="container">
    <Select :options="options" :defaultName="'Выбрать сервис'"/>
    <Select :options="secondOptions" :defaultName="'Тип аккаунта'"/>
  </div>
  
</template>

<script>
import Select from './components/select.vue'

export default {
  name: 'App',
  components: {
    Select,
  },
  data() {
    return {
      options: [
        { group: "",
          groupValues: [{ name: "Хостинг", value: "1" }],
        },
        { group: "Спектр",
          groupValues: [{ name: "Мой сайт на 1C-Битрикс", value: "1" }, { name: "Мой сайт на Joomla!", value: "1" }, { name: "Другой мой сайт на Joomla!", value: "1" }],
        },
        { group: "VPS",
          groupValues: [{ name: "Мой сайт", value: "1" }, { name: "Прокси-сервер", value: "1" }],
        },

      ],

      secondOptions: [
        {groupValues: [{ name: "Хостинг", value: "1" }, { name: "Мой сайт на Joomla!", value: "1" }]},
      ],

      
  }
  }
}
</script>

<style lang="scss">
#app {
  font-family: "PT Sans", sans-serif;
  font-weight: 400;
}
.container {
  display: flex;
  width: 50%;
  justify-content: space-between;
  align-items: center;
  margin: 0 auto;
}
</style>
