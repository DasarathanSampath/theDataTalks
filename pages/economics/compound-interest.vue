<template>
  <!--  eslint-disable  -->
  <client-only>
  <div class="thisLayout">
    <div>
      <h1 class="blogCard__title">
        {{ headA1 }}
        <h2 class="blogCard__desc">
          {{ headA2 }}
        </h2>
      </h1>
      <form @submit.prevent="onSave">
        <AppControlInput v-model="inputValues.oneTimeDeposit">
          {{ headA3 }}
        </AppControlInput>
        <AppControlInput v-model="inputValues.period">
          {{ headA4 }}
        </AppControlInput>
        <AppControlInput v-model="inputValues.rateOfInterest">
          {{ headA5 }}
        </AppControlInput>
        <AppControlInput v-model="inputValues.compoundingPeriod" control-type="dropdownbox">
          {{ headA6 }}
        </AppControlInput>
        <div class="result">
          {{ headA7 }}:  {{ inputValues.oneTimeDeposit }}<br>
          {{ headA8 }}: {{ comopoundInterest }} <br>
          {{ headA9 }}: {{ (+comopoundInterest + +inputValues.oneTimeDeposit) }}
        </div>
      <!-- <div class="input-control">
        <label><slot /></label>
        {{ comopoundInterest }}
      </div> -->
      <!-- <AppControlInput v-model="editedPost.content" control-type="textarea">
        Content
      </AppControlInput> -->
      <!-- <AppButton type="submit">
        Save
      </AppButton>
      <AppButton type="button" style="margin-left: 10px" btn-style="cancel" @click="onCancel">
        Cancel
      </AppButton> -->
      </form>      
    </div>
    <div >
      <h1 class="blogCard__title">
      {{ title }}
    </h1>
    <h2 class="blogCard__desc">
      {{ description }}
    </h2>
    <h3 class="blogCard__date">
      {{ date }}
    </h3>
      <div v-html="content" />
    </div>
  </div>
  </client-only>
</template>

<script>
import AppControlInput from '~/components/AppControlInput.vue'

const fm = require('front-matter')
const md = require('markdown-it')({
  html: true,
  linkify: true,
  typographer: true
})
/* import AppButton from '~/components/AppButton.vue' */
export default {
    components: {
        /* AppButton, */
        AppControlInput
    },
    async asyncData ({ app, params, route, error }) {
      /* const slug = route.params.slug */
      let page
      try {
        page = await import(`~/docs/${app.i18n.locale}/economics/compound-interest.md`)
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
        altLang: attributes.altLang,
        headA1: attributes.headA1,
        headA2: attributes.headA2,
        headA3: attributes.headA3,
        headA4: attributes.headA4,
        headA5: attributes.headA5,
        headA6: attributes.headA6,
        headA7: attributes.headA7,
        headA8: attributes.headA8,
        headA9: attributes.headA9
      }
    },
    data () {
        return {
          inputValues: {
              oneTimeDeposit: '',
              period: '',
              rateOfInterest: '',
              compoundingPeriod: 'Monthly'

            }
        }
      },
      computed: {
          cmCompoundingTimes () {
            let calculatedTimes
              if (this.inputValues.compoundingPeriod === 'HalfYearly') {
                calculatedTimes = 2
              }
              if (this.inputValues.compoundingPeriod === 'Yearly') {
                calculatedTimes = 1
              }
              if (this.inputValues.compoundingPeriod === 'Quarterly') {
                calculatedTimes = 4
              }
              if (this.inputValues.compoundingPeriod === 'Monthly') {
                calculatedTimes = 12
              }
              return calculatedTimes
          },
          comopoundInterest () {
              const interestReceivable = Math.round((((1 + (this.inputValues.rateOfInterest / 100) / this.cmCompoundingTimes) ** (this.inputValues.period * this.cmCompoundingTimes)) - 1) * this.inputValues.oneTimeDeposit)
              return interestReceivable
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
          href: `${process.env.baseUrl + (this.currentLanguage[0].code === 'en' ? '' : '/ta')}/economics/${this.name}`,
          hreflang: this.currentLanguage[0].code
        }
      }

      },

      methods: {
          /* onSave () {
              // eslint-disable-next-line
             console.log(this.editedPost)
          },
          onCancel () {
              this.editedPost.author = ''
          } */
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

<style scoped lang="scss">
.result
{
  display: block;
  width: 80%;
  box-sizing: border-box;
  font: inherit;
  font-weight: bold;
  background-color: lightgray;
  border: 1px solid #ccc;
  padding: 5px;
  text-align: left;
  margin: 10px 40px 10px 10px;
}

.thisLayout{
  display: grid;
  grid-template-columns: 1fr 1fr;
  @media only screen and (max-width: 800px){
    grid-template-columns: 1fr;
  }
}
</style>
