<template>
  <div>
    <div>
      <h1 class="title">nuxt-blog-example</h1>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          rel="noopener noreferrer"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          rel="noopener noreferrer"
          class="button--grey"
        >
          GitHub
        </a>
        <div>
          <div
            v-for="(doc, index) in docs"
            :key="index"
            @click="goToDoc(doc.slug)"
          >
            <h1>{{ doc.title }}</h1>
            <img class="post-image" :src="doc.picture" alt />
            <p>{{ doc.description }}</p>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const docs = await $content('/blog').without(['body', 'toc']).fetch()
    return { docs }
  },
  methods: {
    goToDoc(slug) {
      this.$router.push({ path: `/blog/${slug}` })
    },
  },
}
</script>

<style lang="scss" scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
.post-image {
  width: 200px;
}
</style>
