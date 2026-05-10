<script setup>
const route = useRoute()

const response = await useFetch(
  `http://localhost:1337/api/blog-posts?filters[slug][$eq]=${route.params.slug}`
)
// Slugs are number IDs ranging from 1 to 5 at the moment there are only 5 posts in the database.


let post = null

if (response.data.value &&  response.data.value.data.length > 0 ){
  post = response.data.value.data[0]
}
</script>

<template>
  <div
    v-if="post"
    class="card"
  >
    <NuxtLink
      to="/"
      class="backButton"
    >
      Back to Home
    </NuxtLink>

    <h1 class="title">
      {{ post.Title }}
    </h1>

    <div class="details">
      <div>
        <h3 class="heading">
          Category
        </h3>

        <p>
          {{ post.category }}
        </p>
      </div>

      <div>
        <h3 class="heading">
          Author
        </h3>

        <p>
          {{ post.author }}
        </p>
      </div>
    </div>

    <div
      v-for="block in post.content"
      :key="block.type"
    >
      <p
        v-for="child in block.children"
        :key="child.text"
        class="content"
      >
        {{ child.text }}
      </p>
    </div>
  </div>
</template>

<style>
.card {
  background-color: #000000;
  padding: 50px;
  border-radius: 30px;
  margin-top: 20px;
  margin-bottom: 25px;
  /* min-height: 100vh; */
}

.title {
  font-size: 2rem;
  color: white;
  margin-bottom: 15px;
  text-decoration: underline;
}

.details {
  font-size: 1.5rem;
  display: flex;
  gap: 40px;
  margin-bottom: 25px;
}

.heading {
  color: white;
  font-size: 16px;
  margin-bottom: 5px;
}

.content {
  color: #d1d1d1;
  line-height: 2.3;
  font-size: 1.25rem;
  margin-bottom: 20px;
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