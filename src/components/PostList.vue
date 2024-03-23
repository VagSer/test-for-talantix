<script setup>
import PostListItem from './PostListItem.vue';

defineProps({
  posts: {
    type: Array,
    required: true,
  }
})
</script>

<template>
  <section class="postList" v-if="posts.length">
    <PostListItem 
      v-for="post of posts"
      :key="post.id"
      :post
    />
  </section>
</template>

<style>
@layer appStyle {
  .postList {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
    justify-content: space-around;
  }
}
</style>