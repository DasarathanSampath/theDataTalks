<template>
  <div>
    <!-- eslint-disable -->
    <div>
      <nuxt-link :to="localePath('/')">  
      <ImageResponsive :image-u-r-l="'icon.png'" :height="'50%'" :width="'50%'" :class="'logoImg'"/>
      </nuxt-link>
    </div>
    <div class="header">      
      <nuxt-link :to="localePath('/')" class="logo">  
          <span v-html="$t('header.home')" /> 
      </nuxt-link>
      <nuxt-link :to="localePath('/politics')" class="headerMenu"> <span v-html="$t('header.politics')" /> </nuxt-link>
      <nuxt-link :to="localePath('/economics')" class="headerMenu"> <span v-html="$t('header.economics')" /> </nuxt-link>
      <nuxt-link :to="localePath('/education')" class="headerMenu"> <span v-html="$t('header.education')" /> </nuxt-link>
      <nuxt-link :to="localePath('/others')" class="headerMenu"> <span v-html="$t('header.others')" /> </nuxt-link>
    </div>
    <div class="languageSelect">
      <nuxt-link
      v-for="locale in availableLocales"
      :key="locale.code"
      :to="switchLocalePath(locale.code)"  class="languageText"
      >
        {{ locale.name }}
      </nuxt-link>
  </div>
</div>
</template>

<script>
export default {
    data () {
        return {

        }
    },
    computed: {
    availableLocales () {
    return this.$i18n.locales.filter(i => i.code !== this.$i18n.locale)
  }
}

}
</script>

<style lang="scss">
.header{
  margin-left: 2rem;
  border-bottom: solid;
  border-color: darkgray;
  padding: 1rem 0rem 0rem 0rem;
  @media only screen and (max-width: 800px){
    margin-left: 0rem;
  }
}
.headerMenu{
  padding: 0rem 1.25rem 0rem 0.5rem;
  text-decoration: none;
  font-size: 1.3rem;
  font-weight: 900;
  color: black;

  @media only screen and (max-width: 1024px){
    font-size: 1.1375rem;
    padding: 0rem 1.25rem 0rem 1rem;
  }
  @media only screen and (max-width: 800px){
    font-size: 1rem;
    padding: 0rem 0.5rem 0rem 1rem;
  }
  @media only screen and (max-width: 640px){
    font-size: 1rem;
    padding: 0rem 0.25rem 0rem 0.25rem;

  }
}
.languageSelect{
  margin-left: 2rem;
  padding: 5px 10px 5px 0px;
  @media only screen and (max-width: 800px){
    margin-left: 0rem;
  }
}
.languageText{
  text-decoration: none;
  font-weight: 600;
}

.logo{
    font-size: 2rem;
    font-weight: 900;
    color: black;
    text-decoration: none;
    /* float: left; */
    /* display: grid; */
    /* overflow: hidden; */
/*     grid-template-columns: 1fr 1fr;
    display: grid; */
    margin: 0px;
    padding: 0rem 1.5rem 0rem 0rem;
    @media only screen and (max-width: 1024px){
    font-size: 1.75rem;
    padding: 0rem 1rem 0rem 0rem;
    }
    @media only screen and (max-width: 800px){
    font-size: 1.5rem;
    padding: 0rem 0.25rem 0rem 0rem;
    }
    @media only screen and (max-width: 640px){
    /* font-size: 1.25rem;
    padding: 0rem 0.1rem 0rem 0rem; */
    display: none;
    }
  }

</style>
