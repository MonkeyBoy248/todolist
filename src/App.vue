<template>
  <div class="container">
    <Header @toggleAddTask="toggleAddTask" title="Список дел" />
    <AddTask v-show="showAddTask" @addTask="addTask" v-model="value" />
    <Tasks
      @removeTask="removeTask"
      @taskIsDone="taskIsDone"
      @editTask="editTask"
      :tasks="tasks"
      :done="false"
      title="Активные задачи"
    />
    <Tasks
      :tasks="completeTasks"
      @taskIsDone="taskIsDone"
      @removeTask="removeTask"
      :done="true"
      checked="checked"
      title="Завершенные"
    ></Tasks>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data () {
    return {
      showAddTask: false,
      value: "",
      editedTask: null,
      tasks: [
         {
          id: 0,
          text: "Доделать todoList",
          date: "Today",
        },
        {
          id: 1,
          text: "Понять, что не так с компонентом",
          date: "Today",
        }
      ],
      completeTasks: [],
      counter: 0,
    };
  },
  methods: {
    pad (number) {
      if (number < 10) {
        return "0" + number;
      }
      return number;
    },

    getDate () {
      let currentDate = new Date();
      return `${currentDate.getDate()}.${this.pad(
        currentDate.getMonth()
      )}.${currentDate.getFullYear()}\n
      ${this.pad(currentDate.getHours())}:${this.pad(currentDate.getMinutes())}:${this.pad(currentDate.getSeconds())}`;
    },

    addTask () {
      if (this.value === "") return;

      if (this.editedTask === null) {
        const newTask = {
          id: Math.floor(Math.random() * 100000),
          text: this.value,
          date: this.getDate(),
          done: false,
      }
        this.tasks.push(newTask);

      } else {
        const targetTask = this.tasks.find(
          (task) => task.id === this.editedTask
        );
        targetTask.text = this.value;
        this.editedTask = null;
      }
      this.value = "";
    },

    removeTask (id, done) {
      if (!done) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }else {
        this.completeTasks = this.completeTasks.filter((task) => task.id !== id);
      }
    },

    toggleAddTask () {
      this.showAddTask = !this.showAddTask;
    },

    editTask (id) {
      const targetTask = this.tasks.find((task) => id === task.id);
      this.value = targetTask.text;
      this.editedTask = id;
      this.showAddTask = true;
    },

    taskIsDone (id, done) {
      if (!done) {
        const completedTasks = this.tasks.filter((task) => task.id === id);
        this.completeTasks.push(...completedTasks);
        this.tasks = this.tasks.filter((task) => task.id !== id);
        console.log(id, done);
      } else {
        const activeTasks = this.completeTasks.filter((task) => task.id === id);
        this.tasks.push(...activeTasks);
        this.completeTasks = this.completeTasks.filter(
          (task) => task.id !== id
        );
        console.log(id, done);
      }
    },
  },
};
</script>
