<template>
  <client-only>
    <div>
      <!-- <div v-if="article.type == 'Article'">
        <heading :title="article.title"></heading>
      </div>
      <div v-else-if="article.type == 'Song'">
        <song :title="article.title"></song>
      </div> -->

      <nuxt-content :document="article" />
    </div>
  </client-only>
</template>

<script>
// Typescript Import Example:
// import articleImage from '../components/articleImage.vue'

export default {
  async asyncData ({ $content, params, error }) {
    let article = await $content('/', { deep: true }).where({slug: params.slug}).fetch()

    article = article[0]

    if (!article) {
      return error({ statusCode: 404, message: 'Article not found' })
    }

    return {
      article
    }
  }
}

// import {
//   Component,
//   Vue
// } from "nuxt-property-decorator";

// @Component({
//   async asyncData ({ $content, params, error }: { $content: any, app: any, params: any, error: any }): Promise<any> {
//     let article = await $content('/', { deep: true }).where({slug: params.slug}).fetch()

//     article = article[0]

//     if (!article) {
//       return error({ statusCode: 404, message: 'Article not found' })
//     }

//     return {
//       article
//     }
//   }
// })
// export default class extends Vue {}
</script>
