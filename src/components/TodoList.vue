<template>
  <h1>Meine Todos:</h1>
  <Todo v-for="todo in todos" :todo="todo" :key="todo.id" />
</template>

<script>
import { onMounted, ref } from "@vue/runtime-core";
import { initializeApp } from "firebase/app";
import { getDatabase, ref as fbRef, child, get } from "firebase/database";
import Todo from "@/components/Todo.vue";

export default {
  name: "TodoList",
  setup() {
    const todos = ref([]);

    onMounted(() => {
      var config = {
        apiKey: "AIzaSyCbFdSyJcEoCnQfh8bgCFnyaPtWEAdOvaM",
        authDomain: "todoapp-ca2d3.firebaseapp.com",
        databaseURL:
          "https://todoapp-ca2d3-default-rtdb.europe-west1.firebasedatabase.app",
        projectId: "todoapp-ca2d3",
        storageBucket: "todoapp-ca2d3.appspot.com",
        messagingSenderId: "596776343504",
        appId: "1:596776343504:web:0b9360ec945bde6b814bd5",
      };

      initializeApp(config);
      const dbRef = fbRef(getDatabase());
      get(child(dbRef, `ToDo`))
        .then((snapshot) => {
          if (snapshot.exists()) {
            todos.value = snapshot.val();
          } else {
            console.log("No data available");
          }
        })
        .catch((error) => {
          console.error(error);
        });
    });

    return {
      todos,
    };
  },
  components: {
    Todo,
  },
};
</script>