<script setup>
defineProps({
  post: Object
})
</script>

<template>
  <div class="card">
    <NuxtLink :to="`/post/${post.slug}`">
      <h2 class="title">
        {{ post.Title }}
      </h2>
    </NuxtLink>

    <div class="details">
      <div>
        <h3 class="heading">Category</h3>
        <p>{{ post.category }}</p>
      </div>

      <div>
        <h3 class="heading">Author</h3>
        <p>{{ post.author }}</p>
      </div>
    </div>

    <p class="content">
      {{ post.content?.[0]?.children?.[0]?.text }}
    </p>

    <NuxtLink
      :to="`/post/${post.slug}`"
      class="readMore"
    >
      read more
    </NuxtLink>
  </div>
</template>

<style>
.card {
  background-color: #000000;
  padding: 50px;
  border-radius: 30px;
  margin-top: 20px;
  margin-bottom: 25px;
  min-height: 20vh;
}

.title {
  font-size: 2rem;
  color: white;
  margin-bottom: 15px;
  text-decoration: underline;
}

.title:hover {
  color: #298dff;
}

.details {
  font-size: 1.5rem;
  display: flex;
  gap: 40px;
  margin-bottom: 15px;
}

.heading {
  font-size: 2rem;
  color: white;
  font-size: 16px;
  margin-bottom: 5px;
}

.content {
  color: #d1d1d1;
  line-height: 2;
  font-size: 1.25rem;
}

.readMore {
  display: inline-block;
  margin-top: 15px;
  background-color: #298dff;
  text-decoration: none;
  border: 1px solid #4ea1ff;
  padding: 10px 20px;
  border-radius: 5px;
  color: white;
}

.readMore:hover {
  display: inline-block;
  margin-top: 15px;
  background-color: #75b6ff;
  text-decoration: underline;
}
</style>