<template>
  <div>
    <div class="footer">
      <!-- eslint-disable -->
    <nuxt-link :to="localePath('/')" class="footerMenu"> <span v-html="$t('footer.home')" /> </nuxt-link>
    <nuxt-link :to="localePath('/about')" class="footerMenu"> <span v-html="$t('footer.about')" /> </nuxt-link>
    <nuxt-link :to="localePath('/contact')" class="footerMenu"> <span v-html="$t('footer.contact')" /> </nuxt-link>
    <nuxt-link :to="localePath('/disclaimer')" class="footerMenu"> <span v-html="$t('footer.disclaimer')" /> </nuxt-link>
    <nuxt-link :to="localePath('/privacy')" class="footerMenu"> <span v-html="$t('footer.privacy')" /> </nuxt-link>
  </div>
  <div class="footerSlogan">
    <span v-html="$t('footer.slogan')" />
  </div>
</div>
</template>

<script>
export default {
    data () {
        return {

        }
    }

}
</script>

<style lang="scss">
.footer{
  margin-left: 2rem;
  /* border-top: solid; */
  /* margin-right:250px; */
  border-color: darkgray;
  padding: 0rem 0rem 0.1rem 0rem;
/*   @media only screen and (max-width: 1024px){
    margin-right:50px;
  }*/
  @media only screen and (max-width: 800px){
    margin-left: 0rem;
  }
}
.footerMenu{
  padding: 0rem 1.5rem 0rem 1rem;
  text-decoration: none;
  font-size: 1.1rem;
  font-weight: 900;
  color: black;
  @media only screen and (max-width: 1024px){
    font-size: 1rem;
    padding: 0rem 1rem 0rem 1rem;
  }
  @media only screen and (max-width: 800px){
    font-size: 1rem;
    padding: 0rem 0.25rem 0rem 0rem;
  }
  @media only screen and (max-width: 640px){
    font-size: 0.8rem;
    padding: 0rem 0.25rem 0rem 0rem;

  }
}

.footerSlogan{
  padding: 0rem 0rem 0rem 0rem;
  text-decoration: none;
  /* margin-left: 4rem; */
  text-align: left;
  /* float: left; */
  font-size: 0.8rem;
  font-weight: 900;
  color: black;
}

</style>
