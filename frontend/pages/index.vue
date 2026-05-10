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

