<script setup>
defineProps({
  post: Object
})
</script>

<template>
  <div>
    <NuxtLink :to="`/post/${post.slug}`">
      <h2>
        {{ post.Title }}
      </h2>
    </NuxtLink>

    <div>
      <span>
        {{ post.category }}
      </span>

      <span>
        {{ post.author }}
      </span>
    </div>

    <p>
      {{ post.content?.[0]?.children?.[0]?.text }}
    </p>

    <NuxtLink :to="`/post/${post.slug}`">
      Read More →
    </NuxtLink>
  </div>
</template>