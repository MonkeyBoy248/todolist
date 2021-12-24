<template>
  <form @submit.prevent="addTask" class="add-task">
    <fieldset class="add-task__fields">
      <label class="add-task__description-label" for="description">
        Описание
      </label>
      <input
        type="text"
        name="description"
        id="description"
        class="add-task__description"
        placeholder="Описание задачи"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
      />
      <button @click="addTask" type="button" class="button button_save-task">
        Сохранить задачу
      </button>
    </fieldset>
  </form>
</template>

<script>
export default {
  name: "AddTask",
  props: ["modelValue"],
  methods: {
    addTask () {
      this.$emit("addTask");
    },
  },
}
</script>
