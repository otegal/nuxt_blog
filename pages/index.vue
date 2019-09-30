<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <div class="text-center">
      <ul>
        <li v-for="post in posts" :key="post.fields.slug">{{ post.fields.title }}</li>
      </ul>
    </div>
  </v-layout>
</template>

<script>
import { createClient } from "~/plugins/contentful.js";

const client = createClient()

export default {
  async asyncData ({ env, params }) {
    return await client.getEntries({
      'content_type': env.CTF_BLOG_POST_TYPE_ID,
      order: '-fields.publishedAt',
    }).then(entries => {
      console.log(entries)
      return { posts: entries.items }
    })
    .catch(
      console.error
    )
  }
}
</script>
