<template>
  <div>
    <ul style="padding: 0; list-style-type: none;">
      <div class="blogLayout">
        <div>
          <li v-for="blog in blogs.slice(0,2)" :key="blog.name" :blog="blog" class="blogList">
            <nuxt-link :to="localePath(`/${section}/${blog.name}`)" class="nuxtLink">
              <div class="blogCardH">
                <ImageResponsive :image-u-r-l="`${section}/${blog.name}/_thumbnail.png`" :height="'100%'" :width="'100%'" />
                <div>
                  <h1 class="blogCard__title">
                    {{ blog.title }}
                  </h1>
                  <h2 class="blogCard__desc">
                    {{ blog.desc }}
                  </h2>
                  <h1 class="blogCard__date">
                    {{ blog.date }}
                  </h1>
                  <h2 class="blogCard__desc">
                    {{ blog.imgDesc }}
                  </h2>
                </div>
              </div>
            </nuxt-link>
          </li>
        </div>
        <div>
          <li v-for="blog in blogs.slice(2,4)" :key="blog.name" :blog="blog" class="blogList">
            <nuxt-link :to="localePath(`/${section}/${blog.name}`)" class="nuxtLink">
              <div class="blogCardV">
                <ImageResponsive :image-u-r-l="`${section}/${blog.name}/_thumbnail.png`" />
                <div>
                  <h1 class="blogCard__title">
                    {{ blog.title }}
                  </h1>
                  <h2 class="blogCard__desc">
                    {{ blog.desc }}
                  </h2>
                  <h1 class="blogCard__date">
                    {{ blog.date }}
                  </h1>
                </div>
              </div>
            </nuxt-link>
          </li>
        </div>
        <div>
          <li v-for="blog in blogs.slice(4,6)" :key="blog.name" :blog="blog" class="blogList">
            <nuxt-link :to="localePath(`/${section}/${blog.name}`)" class="nuxtLink">
              <div class="blogCardV2">
                <h1 class="blogCard__title">
                  {{ blog.title }}
                </h1>
                <h2 class="blogCard__desc">
                  {{ blog.desc }}
                </h2>
              </div>
            </nuxt-link>
          </li>
        </div>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    blogs: {
      type: Array,
      required: true
    },
    section: {
      type: String,
      required: true
    }/* ,
    firstBlog: {
      type: Object,
      required: true
    } */
  }
}
</script>

<style lang="scss">

</style>
