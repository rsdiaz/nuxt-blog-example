<template>
  <div>
    <section class="hero is-medium is-link">
      <div class="hero-body">
        <div class="container">
          <h1 class="title is-1 is-spaced">
            Hola!
          </h1>
          <figure class="image my-6">
            <img
              class="profile-pic is-rounded has-shadow"
              src="https://res.cloudinary.com/rserrano/image/upload/v1598652059/roberto-serrano-desarrolloweb-tarragona.jpg"
              alt="Roberto Serrano desarrollo web Tarragona"
            />
          </figure>
          <h2 class="subtitle">
            <p>
              Mi nombre es Roberto Serrano.
            </p>
            <p>
              Soy un desarrollador web viviendo en Tarragona, España.
            </p>
            <p>
              Desde 2012, llevo desarrollando aplicaciones web y he ayudado a
              muchas personas a lograr cosas innovadoras en la Web.
            </p>
            <p>
              Principalmente trabajo con herramientas y frameworks modernos como
              Wordpress, VueJs, Angular...
            </p>
            <p>
              Ultimamente enamorado de JAMStack.
            </p>
            <p>
              Puedes leer más
              <a href="/sobre-mi">sobre mi</a> o consultar algunos de mis
              <a href="/proyectos">proyectos.</a>
            </p>
          </h2>
        </div>
      </div>
    </section>
    <div class="section">
      <h2 class="title is-4">📒 Ultimos artículos en el blog</h2>
      <div class="links">
        <div>
          <div
            v-for="(doc, index) in docs"
            :key="index"
            @click="goToDoc(doc.slug)"
          >
            <h2 class="has-text-weight-bold">
              <span class="has-text-weight-bold is-size-5">#</span>
              {{ doc.title }}
              -
              <span class="has-text-weight-normal is-italic">
                {{ formatDate(doc.updatedAt) }}
              </span>
            </h2>
            <!-- <img class="post-image" :src="doc.picture" alt />
            <p>{{ doc.description }}</p> -->
          </div>
        </div>
        <nuxt-link to="/blog">
          Leer todas las entradas
        </nuxt-link>
      </div>
    </div>
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
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('es', options)
    },
  },
  head: {
    title: 'Mi blog con Nuxtjs',
  },
}
</script>

<style lang="scss" scoped>
.links {
  padding-top: 15px;
  h2 {
    margin-bottom: 1rem;
    cursor: pointer;
  }
}
.post-image {
  width: 200px;
}
</style>
