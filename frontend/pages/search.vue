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
  <div class="container">
    <NuxtLink
      to="/"
      class="backButton"
    >
      Back to Home
    </NuxtLink>

    <h1 class="pageTitle">
      Search Posts
    </h1>

    <input
      v-model="searchTerm"
      placeholder="Search by title or author"
      class="searchInput"
    />

    <Card
      v-for="post in getFilteredPosts()"
      :key="post.id"
      :post="post"
    />
  </div>
</template>

<style>
.container {
  min-height: 100vh;
  background-color: #000000;
  padding: 40px;
}

.pageTitle {
  color: white;
  font-size: 3rem;
  margin-bottom: 25px;
}

.searchInput {
  width: 100%;
  padding: 15px;
  font-size: 1rem;
  background-color: #1a1a1a;
  border: 1px solid #4ea1ff;
  border-radius: 10px;
  color: white;
  margin-bottom: 30px;
}

.searchInput:focus {
  outline: none;
  border: 1px solid #d9ebff;
}

.backButton {
  display: inline-block;
  margin-bottom: 30px;
  background-color: #298dff;
  text-decoration: none;
  border: 1px solid #4ea1ff;
  padding: 10px 20px;
  border-radius: 5px;
  color: white;
}

.backButton:hover {
  background-color: #75b6ff;
  text-decoration: underline;
}
</style>