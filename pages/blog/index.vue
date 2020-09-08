<template>
  <section class="section">
    <h1 class="title is-1 has-text-centered-touch">Blog</h1>
    <div class="content">
      <div
        v-for="(article, index) in articles"
        :key="index"
        class="card blog-list"
      >
        <div class="card-image">
          <figure class="image is-4by3">
            <img :src="article.picture" loading="lazy" />
          </figure>
        </div>
        <div class="blog-excerpt">
          <h2 class="title is-4">
            <NuxtLink :to="`/blog/${article.slug}`">
              {{ article.title }}
            </NuxtLink>
          </h2>
          <p>{{ formatDate(article.createdAt) }}</p>
          <p>{{ article.description }}</p>
          <div class="blog-excerpt-bottom">
            <NuxtLink :to="`/blog/${article.slug}`">
              Leer más
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  async asyncData({ $content }) {
    const articles = await $content('/blog').sortBy('createdAt', 'desc').fetch()
    return { articles }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('es', options)
    },
  },
}
</script>
<style lang="scss">
section.section {
  h1.title {
    margin-bottom: 3rem;
  }
  h2.title {
    margin-bottom: 0.5714em;
  }
}
.content {
  figure {
    margin-left: 0;
    margin-right: 0;
  }
}
</style>
