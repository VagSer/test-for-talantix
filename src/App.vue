<script setup>
import { onMounted, ref, computed } from 'vue';
import PostList from './components/PostList.vue';
import SearchInput from './components/SearchInput.vue';
import AppLoader from './components/AppLoader.vue';
import ErrorMessage from './components/ErrorMessage.vue';

const allPosts = ref([]);
const allUsers = ref([]);
const authorName = ref('');
const isLoading = ref(false);

const visiblePosts = computed(() => {
  return allPosts.value.filter(post => 
    post.author.toLowerCase().includes(authorName.value.toLocaleLowerCase()))
})

const showError = computed(() => !isLoading.value && !visiblePosts.value.length)

const uploadData = async () => {
  isLoading.value = true;
  const dataPosts = await fetch('https://jsonplaceholder.typicode.com/posts')
    .then(response => response.json());
  const dataUsers = await fetch('https://jsonplaceholder.typicode.com/users')
    .then(response => response.json());
  dataPosts.forEach(post => {
    const author = dataUsers.find(user => user.id === post.userId);
    allPosts.value.push({...post, author: author.name});
  })
  allUsers.value = [...dataUsers];
  isLoading.value = false;
}

onMounted(() => {
  uploadData();
})
</script>

<template>
  <SearchInput v-model:value="authorName"/>
  <AppLoader v-if="isLoading"/>
  <PostList :posts="visiblePosts"/>
  <ErrorMessage v-if="showError"/>
</template>
