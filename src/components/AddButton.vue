<template>
  <button @click="showAddTask" type="button" class="button">{{ content }}</button>
</template>

<script>
export default {
  name: "Button",
  props: ["content"],
  methods: {
    showAddTask () {
      this.$emit ("toggleAddTask");
    }
  }
}
</script>
