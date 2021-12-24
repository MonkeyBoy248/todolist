<template>
  <section class="tasks">
    <div class="tasks__main-info">
      <h3 class="tasks__header">{{ title }}</h3>
      <span class="tasks__tasks-counter">{{ tasks.length }}</span>
    </div>
    <ul class="tasks__tasks-list">
      <li :key="task.id" v-for="task in tasks" class="tasks__list-item">
        <Task
          @removeTask="$emit('removeTask', task.id, done)"
          @taskIsDone="$emit('taskIsDone', task.id, done)"
          @editTask="$emit('editTask', task.id)"
          :task="task"
          :done="done"
          :checked="checked"
        />
      </li>
    </ul>
  </section>
</template>

<script>
import Task from "./Task";

export default {
  name: "Tasks",
  props: {
    tasks: Array,
    title: String,
    done: Boolean,
    checked: String,
  },
  components: {
    Task,
  },
}
</script>
