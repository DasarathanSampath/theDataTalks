<template>
  <div>
    <BlogCards
      :blogs="results"
    />
  </div>
</template>

<script>
import BlogCards from '~/components/blogCardLayoutHome.vue'
import blogsEnPolitics from '~/docs/en/politics/blogsEn.js'
import blogsTaPolitics from '~/docs/ta/politics/blogsTa.js'
import blogsEnEconomics from '~/docs/en/economics/blogsEn.js'
import blogsTaEconomics from '~/docs/ta/economics/blogsTa.js'
import blogsEnEducation from '~/docs/en/education/blogsEn.js'
import blogsTaEducation from '~/docs/ta/education/blogsTa.js'
import blogsEnOthers from '~/docs/en/others/blogsEn.js'
import blogsTaOthers from '~/docs/ta/others/blogsTa.js'
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
  const blogsPolitics1 = app.i18n.locale === 'en' ? blogsEnPolitics : blogsTaPolitics
  const blogsPolitics = blogsPolitics1.slice(0, 3)
  const blogsEconomics1 = app.i18n.locale === 'en' ? blogsEnEconomics : blogsTaEconomics
  const blogsEconomics = blogsEconomics1.slice(0, 2)
  const blogsEducation1 = app.i18n.locale === 'en' ? blogsEnEducation : blogsTaEducation
  const blogsEducation = blogsEducation1.slice(0, 4)
  const blogsOthers1 = app.i18n.locale === 'en' ? blogsEnOthers : blogsTaOthers
  const blogsOthers = blogsOthers1.slice(0, 1)
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
  const fileContent = fm(page.default)
  const attributes = fileContent.attributes
  async function asyncImport (blogNamePolitics/* , blogNameEconomics */) {
      const wholeMDPolitics = await import(`~/docs/${app.i18n.locale}/politics/${blogNamePolitics}.md`)
      const resPolitics = fm(wholeMDPolitics.default)
      return resPolitics.attributes
    }
  async function asyncImport2 (blogNameEconomics) {
      const wholeMDEconomics = await import(`~/docs/${app.i18n.locale}/economics/${blogNameEconomics}.md`)
      const resEconomics = fm(wholeMDEconomics.default)
      return resEconomics.attributes
    }
  async function asyncImport3 (blogNameEducation) {
      const wholeMDEducation = await import(`~/docs/${app.i18n.locale}/education/${blogNameEducation}.md`)
      const resEducation = fm(wholeMDEducation.default)
      return resEducation.attributes
    }
  async function asyncImport4 (blogNameOthers) {
      const wholeMDOthers = await import(`~/docs/${app.i18n.locale}/others/${blogNameOthers}.md`)
      const resOthers = fm(wholeMDOthers.default)
      return resOthers.attributes
    }
  return Promise.all(blogsPolitics.map(blog => asyncImport(blog)).concat(blogsEconomics.map(blog2 => asyncImport2(blog2)).concat(blogsEducation.map(blog3 => asyncImport3(blog3))).concat(blogsOthers.map(blog4 => asyncImport4(blog4)))))
    .then((results) => {
      return {
        results,
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
  data () {
    return {

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

<style lang="scss">

</style>
