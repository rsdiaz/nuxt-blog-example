<template>
  <div>
    <Header />
    <article class="section is-medium">
      <header>
        <div class="title-container mb-4">
          <div
            id="blog-post-cover"
            class="background-cover"
            :style="{ backgroundImage: 'url(' + article.picture + ')' }"
          >
            <div class="background-shroud">
              <p class="title has-text-centered is-2">
                {{ article.title }}
              </p>
              <p class="date has-text-centered has-text-weight-light">
                Publicado el {{ formatDate(article.updatedAt) }}
              </p>
            </div>
          </div>
          <div class="section pt-2 pb-2">
            <div class="container">
              <p class="has-text-centered has-text-grey is-italic">
                {{ article.description }}
              </p>
            </div>
          </div>
        </div>
      </header>
      <!-- <img class="image" :src="article.picture" :alt="article.alt" /> -->
      <div class="container">
        <div class="box has-background-info-light">
          <h3 class="title is-5">Contenido</h3>
          <nav>
            <ul>
              <li
                v-for="link of article.toc"
                :key="link.id"
                :class="{
                  'has-text-weight-bold': link.depth === 2,
                  'pl-2 has-text-weight-normal': link.depth === 3,
                }"
              >
                <NuxtLink :to="`#${link.id}`">{{ link.text }}</NuxtLink>
              </li>
            </ul>
          </nav>
        </div>
        <!-- markdown content -->
        <nuxt-content :document="article" />
        <!-- content author component -->
        <author :author="article.author" />
      </div>
    </article>
    <Footer />
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content('blog', params.slug).fetch()
    return { article }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('es', options)
    },
  },
}
</script>
<style lang="scss" scoped>
.nuxt-content {
  h2,
  h3,
  h4 {
    font-weight: bold;
    margin-top: 0.5rem;
    margin-bottom: 0.25rem;
    line-height: 1.25;
  }
}
.nuxt-content h2 {
  font-size: 1.875rem;
}
.nuxt-content h3 {
  font-size: 1.5rem;
}
.nuxt-content p {
  margin-bottom: 20px;
}
.nuxt-content-highlight {
  margin: 1.2rem 0;
}
</style>
