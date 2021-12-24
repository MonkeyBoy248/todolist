<template>
  <header class="header">
    <div class="header__inner">
      <h1 class="header__title">{{ title }}</h1>
      <AddButton
        @toggleAddTask="$emit('toggleAddTask')"
        content="Добавить задачу"
      ></AddButton>
    </div>
  </header>
</template>

<script>
import AddButton from "./AddButton.vue";

export default {
  name: "Header",
  props: {
    title: String
  },
  components: {
    AddButton,
  }
}
</script>
