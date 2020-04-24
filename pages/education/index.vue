<template>
  <div>
    <BlogCards
      :blogs="blogs"
      section="education"
    />
  </div>
</template>

<script>
import BlogCards from '~/components/blogCardLayout.vue'
import blogsEn from '~/docs/en/education/blogsEn.js'
import blogsTa from '~/docs/ta/education/blogsTa.js'
const fm = require('front-matter')
const md = require('markdown-it')({
  html: true,
  linkify: true,
  typographer: true
})
export default {
  components: {
    BlogCards
  },
  async asyncData ({ app, params, error }) {
  const blogs = app.i18n.locale === 'en' ? blogsEn : blogsTa
        /* const slug = route.params.slug */
      let page
      try {
        page = await import(`~/docs/${app.i18n.locale}/index.md`)
      } catch (err) {
          if (err.response.status !== 404) {
          return error({ statusCode: 500, message: '500 error' })
        }
        return error({ statusCode: 404, message: '404 error' })
      }
  /* const fileImport = await import(`~/docs/${app.i18n.locale}/index.md`) */
  const fileContent = fm(page.default)
  const attributes = fileContent.attributes
  async function asyncImport (blogName) {
      const wholeMD = await import(`~/docs/${app.i18n.locale}/education/${blogName}.md`)
      const res = fm(wholeMD.default)
      return res.attributes
    }
    return Promise.all(blogs.map(blog => asyncImport(blog)))
    .then((res) => {
      return {
        blogs: res,
        title: attributes.title,
        description: attributes.desc,
        date: attributes.date,
        noMainImage: attributes.noMainImage,
        content: md.render(fileContent.body),
        name: attributes.name,
        imgDesc: attributes.imgDesc,
        altLang: attributes.altLang
      }
    })
  },
  computed: {
      ogImage () {
        return `${process.env.baseUrl}/images/education/${this.name}/_thumbnail.png`
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
          href: `${process.env.baseUrl + (this.currentLanguage[0].code === 'en' ? '' : '/ta')}/education/${this.name}`,
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

<style lang="scss">

</style>
