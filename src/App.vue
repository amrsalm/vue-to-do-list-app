<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer">
      <!--  -->
    </v-navigation-drawer>

    <v-app-bar app color="blue" dark>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>FrameWorks</v-toolbar-title>
      <addTask></addTask>
    </v-app-bar>

    <v-main>
      <TodoList v-bind:tasks="tasks"></TodoList>
      <v-snackbar v-model="snackbar" color="green">
        {{ text }}

        <template v-slot:action="{ attrs }">
          <v-btn color="black" text v-bind="attrs" @click="snackbar = false">
            Close
          </v-btn>
        </template>
      </v-snackbar>
    </v-main>
  </v-app>
</template>

<script>
import addTask from "./components/addTask.vue";
import TodoList from "./components/TodoList.vue";

export default {
  components: { addTask, TodoList },
  data: function () {
    return {
      add: true,
      snackbar: false,
      snackbar1: false,
      text: "Task added Successfully ",
      tasks: [],
    };
  },
  watch: {
    tasks: {
      handler() {
        console.log("Todo Items array changed!");
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
      deep: true,
    },
  },
  mounted() {
    console.log("App Mounted");
    if (localStorage.getItem("tasks"))
      this.tasks = JSON.parse(localStorage.getItem("tasks"));
  },
};
</script>
