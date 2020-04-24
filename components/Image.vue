<template lang="html">
  <div
    v-lazy-container="{ selector: 'img' }"
    :class="`image-placeholder ${isRounded}`"
  >
    <img
      :data-src="imageRequired"
      :data-loading="imageRequired.placeholder"
      :width="width"
      :height="height"
      :class="classes"
      :alt="alt"
    >
  </div>
</template>

<script>
export default {
  props: {
    imageURL: {
      type: String,
      required: true
    },
    alt: {
      type: String,
      default: "'Blog picture'"
    },
    width: {
      type: String,
      /* required: true, */
      default: '100%'
    },
    height: {
      type: String,
      default: '100%'
    },
    classes: {
      type: String,
      default: 'cardThumbnail'
      /* default: 'elevate-cover-img' */
    },
    rounded: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    imageRequired () {
      return require(`@/assets/images/${this.imageURL}`)
    },
    isRounded () {
      return this.rounded ? 'image-placeholder--rounded' : ''
    }
  }
}
</script>

<style scoped lang="scss">

.image-placeholder {
  overflow: hidden;
  line-height: 0;
  &--rounded {
    border-radius: 100%;
  }
}

img {
  transition: all ease .3s;
  opacity: 0;
  border-radius: 2%;
  &[lazy='loading'] {
    opacity: 1;
    filter: blur(15px);
  }
  &[lazy='loaded'] {
    opacity: 1;
  }
}

/* .elevate-cover-img {
    align-items: center;
    justify-content: center;
    padding-top: 0.5rem;
    padding: 0.2rem 0.5rem 0.2rem 1rem;
    @media (max-width: 960px)
    {
      padding: 0rem 0rem 0rem 0rem;
    }
} */

</style>
