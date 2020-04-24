<template>
  <div>
    <div class="layoutGrid">
      <div>
      <!-- adds by google -->
      </div>

      <div>
        <TheHeader />
        <nuxt />
        <TheFooter />
      </div>

      <div>
      <!-- adds by google -->
      </div>
    </div>
  </div>
</template>

<script>
import TheHeader from '~/components/navigation/TheHeader'
import TheFooter from '~/components/navigation/TheFooter'
export default {
  components: {
    TheHeader,
    TheFooter
  },
  data () {
    return {

    }
  }
}
</script>

<style>

</style>
