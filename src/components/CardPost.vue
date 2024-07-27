<script setup>

const props = defineProps({
    userId: Number,
    id: Number,
    urlImage: {
        type: String,
        default: 'https://i.imgur.com/ipKVbRp.jpeg'
    },
    title: String,
    body: String
})

</script>

<template>

<div class="card" style="width: 18rem;" :userId="userId" :postId="id">
  <img :src="urlImage" class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">{{ title }}</h5>
    <p class="card-text">{{ body }}</p>
    <a href="#" class="btn btn-primary">VER POST</a>
  </div>
</div>

</template>