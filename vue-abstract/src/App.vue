<template>
  <div>
    <!-- Основной шаблон (Options API) -->
    <h1>{{ title }}</h1>
    <button @click="increment">+</button>
    <p>Count: {{ count }}</p>
    <p>Удвоенный count: {{ doubledCount }}</p>

    <!-- Composition API примеры -->
    <p v-if="isVisible">Виден при isVisible = true</p>
    <p v-else>Иначе показывается это</p>

    <ul>
      <li v-for="(item, index) in items" :key="index">{{ item.name }}</li>
    </ul>

    <a :href="url">Ссылка (v-bind)</a>
    <button @click="handleClick">Клик (v-on)</button>
    <input v-model="inputText" placeholder="v-model example" />
    <div ref="divRef">Элемент для ref</div>
  </div>
</template>

<script>
export default {
  // Options API
  data() {
    return {
      title: "Vue App",
      count: 0,
      users: [{ name: "Alex" }, { name: "Max" }],
      url: "https://vuejs.org",
    };
  } /* Реактивные данные */,

  /*   props: {
    message: {
      type: String,
      default: "Hello",
    },
    countProp: Number,
  }, */

  /*   emits: ["customEvent"], */

  methods: {
    /* Методы */
    increment() {
      this.count++;
    },
    handleClick() {
      this.$emit("customEvent", "Данные");
    },
  },

  computed: {
    /* вычисляемые свойства */
    doubledCount() {
      return this.count * 2;
    },
  },

  watch: {
    /* отслеживание изменений */
    count(newVal, oldVal) {
      console.log(`Count changed: ${oldVal} → ${newVal}`);
    },
  },

  created() {
    /* Хуки жизненного цикла */
    console.log("Компонент создан (Options API)");
  },

  // Composition API
  setup() {
    /*  точка входа для Composition API */
    console.log("Composition API setup");

    // Реактивные переменные
    const inputText = ref("");
    const state = reactive({
      isVisible: true,
      items: [{ name: "Vue" }, { name: "React" }],
    });

    // Refs для DOM
    const divRef = ref(null);

    // watchEffect
    watchEffect(() => {
      console.log("inputText:", inputText.value);
    });

    // Provide/inject
    provide("theme", "dark");

    return {
      inputText,
      ...toRefs(state),
      divRef,
    };
  },
};
</script>

<style scoped>
/* Локальные стили */
div {
  color: #42b983;
}

div button {
  background: #35495e;
  color: white;
}

ul {
  color: v-bind('props.message.includes("Hello") ? "green" : "red"');
}
</style>
