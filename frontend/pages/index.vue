<script setup>
const { data } = await useFetch(
  'http://localhost:1337/api/blog-posts'
)

const selectedCategory = ref('All')

function getCategories() {
  const categoryList = ['All']

  if (!data.value || !data.value.data) {
    return categoryList
  }

  for (let i = 0; i < data.value.data.length; i++) {
    const post = data.value.data[i]

    let exists = false

    for (let j = 0; j < categoryList.length; j++) {
      if (categoryList[j] === post.category) {
        exists = true
        break
      }
    }

    if (!exists) {
      categoryList.push(post.category)
    }
  }

  return categoryList
}

function getFilteredPosts() {
  const results = []

  if (!data.value || !data.value.data) {
    return results
  }

  if (selectedCategory.value === 'All') {
    return data.value.data
  }

  for (let i = 0; i < data.value.data.length; i++) {
    const post = data.value.data[i]

    if (post.category === selectedCategory.value) {
      results.push(post)
    }
  }

  return results
}
</script>

<template>
  <div class="mainOverview">
    <NuxtLink
      to="/search"
      class="searchButton"
    >
      Go to Search Page
    </NuxtLink>

    <h1>
      Blog Posts
    </h1>

    <select v-model="selectedCategory">
      <option
        v-for="category in getCategories()"
        :key="category"
      >
        {{ category }}
      </option>
    </select>

    <Card
      v-for="post in getFilteredPosts()"
      :key="post.id"
      :post="post"
    />
  </div>
</template>

<style>
body {
  margin: 0;
  background-color: #0f0f0f;
  color: white;
}

.mainOverview {
  max-width: 900px;
  margin: auto;
  padding: 30px;
}

h1 {
  font-size: 40px;
  margin-bottom: 20px;
  color: white;
}

select {
  background-color: #1e1e1e;
  color: white;
  border: 1px solid #333;
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 25px;
  width: 200px;
}

.searchButton {
  display: inline-block;
  margin-bottom: 30px;
  background-color: #298dff;
  text-decoration: none;
  border: 1px solid #4ea1ff;
  padding: 10px 20px;
  border-radius: 5px;
  color: white;
}

.searchButton:hover {
  background-color: #75b6ff;
  text-decoration: underline;
}
</style>