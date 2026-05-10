<script setup>
const { data } = await useFetch(
  'http://localhost:1337/api/blog-posts'
)

const searchTerm = ref('')

function getFilteredPosts() {
  const results = []

  if (!data.value || !data.value.data) {
    return results
  }

  const search = searchTerm.value.toLowerCase()

  for (let i = 0; i < data.value.data.length; i++) {
    const post = data.value.data[i]

    const title = post.Title.toLowerCase()
    const author = post.author.toLowerCase()

    if (
      title.includes(search) ||
      author.includes(search)
    ) {
      results.push(post)
    }
  }

  return results
}
</script>

<template>
  <div>
    <h1>
      Search Posts
    </h1>

    <input
      v-model="searchTerm"
      placeholder="Search by title or author"
    />

    <Card
      v-for="post in getFilteredPosts()"
      :key="post.id"
      :post="post"
    />
  </div>
</template>