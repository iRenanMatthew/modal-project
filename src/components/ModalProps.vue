<template>
  <!-- Click Event Modifiers -->
  <!-- It will close only if backdrop was clicked -->
  <div class="backdrop" @click.self="closeModal">
    <div
      class="modal"
      :class="{ sale: theme === 'sale', default: theme === '' }"
    >
      <h1>I am Using Props</h1>
      <h1>{{ header }}</h1>
      <p>{{ text }}</p>
    </div>
  </div>
</template>

<script>
// Using props
export default {
  props: ["header", "text", "theme"],
  methods: {
    // EMITS (Passing data from modal to component)
    closeModal() {
      this.$emit("close");
    },
  },
};
</script>

<style>
.modal {
  width: 400px;
  padding: 20px;
  margin: 100px auto;
  background: white;
  border-radius: 10px;
}

.backdrop {
  top: 0;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}

.modal.sale {
  background: crimson;
  color: white;
}

.modal.sale h1 {
  color: white;
}
</style>
