<script setup>
const route = useRoute()

const response = await useFetch(
  `http://localhost:1337/api/blog-posts?filters[slug][$eq]=${route.params.slug}`
)
// Slugs are number IDs ranging from 1 to 5, at the moment there are only 5 posts in the database.

let post = null

if (response.data.value && response.data.value.data.length > 0) {
  post = response.data.value.data[0]
}
</script>

<template>
  <div v-if="post">
    <h1>{{ post.Title }}</h1>

    <p>
      Author: {{ post.author }}
    </p>

    <p>
      Category: {{ post.category }}
    </p>

    <div
      v-for="block in post.content"
      :key="block.type"
    >
      <p
        v-for="child in block.children"
        :key="child.text"
      >
        {{ child.text }}
      </p>
    </div>
  </div>  
</template>