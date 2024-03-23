<script setup>
defineProps({
  post: {
    type: Object,
  }
})
</script>

<template>
  <article class="card card-body">
    <h4 class="card-title">{{ post.title }}</h4>
    <p class="card-text">
      {{ post.body }}
    </p>
    <h5 class="card-subtitle">{{ post.author }}</h5>
  </article>
</template>

<style>
@layer appStyle {
  .card {
    width: min(90%, 300px);
    display: flex;
    justify-content: space-between;
  }
  .card-title {
    color: var(--blue-color);
  }
  .card-subtitle {
    color: gray;
    font-size: 1rem;
  }
}
</style>