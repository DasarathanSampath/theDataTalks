<template>
  <div class="blogContent">
    <h1 class="blogCard__title">
      {{ title }}
    </h1>
    <h2 class="blogCard__desc">
      {{ description }}
    </h2>
    <h3 class="blogCard__date">
      {{ date }}
    </h3>
    <!-- eslint-disable-next-line -->
    <div v-html="content" />
  </div>
</template>

<script>
const fm = require('front-matter')
const md = require('markdown-it')({
  html: true,
  linkify: true,
  typographer: true
})
export default {
    async asyncData ({ app, params, route, error }) {
      const slug = route.params.slug
      let page
      try {
        page = await import(`~/docs/${app.i18n.locale}/${slug}.md`)
      } catch (err) {
          if (err.response.status !== 404) {
          return error({ statusCode: 500, message: '500 error' })
        }
        return error({ statusCode: 404, message: '404 error' })
      }
      const fileContent = fm(page.default)
      const attributes = fileContent.attributes
      return {
        title: attributes.title,
        description: attributes.desc,
        date: attributes.date,
        noMainImage: attributes.noMainImage,
        content: md.render(fileContent.body),
        name: attributes.name,
        altLang: attributes.altLang
      }
    },

    computed: {
      ogImage () {
        return `${process.env.baseUrl}/images/politics/${this.name}/_thumbnail.png`
      },
      pageTitle () {
        return this.title
      },
      currentLanguage () {
        return this.$i18n.locales.filter(i => i.code !== this.$i18n.locale)
      },
      hreflang () {
        if (!this.altLang) {
          return ''
        }
        return {
          hid: 'alternate-hreflang-' + this.currentLanguage[0].iso,
          rel: 'alternate',
          href: `${process.env.baseUrl + (this.currentLanguage[0].code === 'en' ? '' : '/ta')}/politics/${this.name}`,
          hreflang: this.currentLanguage[0].code
        }
      }
    },
    head () {
      return {
        title: this.pageTitle,
        htmlAttrs: {
          lang: this.$i18n.locale
        },
        meta: [
          { name: 'author', content: 'Dasarathan Sampath' },
          { name: 'description', property: 'og:description', content: this.description, hid: 'description' },
          { property: 'og:title', content: this.pageTitle },
          { property: 'og:image', content: this.ogImage },
          { name: 'twitter:description', content: this.description },
          { name: 'twitter:image', content: this.ogImage }
        ],
        link: [
          this.hreflang
        ]
      }
    }
}
</script>
