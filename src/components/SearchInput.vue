<script setup>
const emit = defineEmits(['update:value']);

defineProps({
  value: {
    type: String,
    required: true,
  }
})

const updateValue = (event) => {
  emit('update:value', event.target.value)
}
</script>

<template>
  <div class="input-group mb-3">
    <span class="input-group-text" id="basic-addon1">
      <i class="bi bi-search"></i>
    </span>
    <input 
      :value
      type="text"
      class="form-control"
      placeholder="Username"
      aria-label="Username"
      aria-describedby="basic-addon1"
      @input="updateValue"
    >
  </div>
</template>

<style>
@layer appStyle {
  .input-group {
    position: sticky;
    top: 0;
    z-index: 2;
    box-shadow: 0 0 4px black;
    border-radius: var(--bs-border-radius);
  }
}
</style>