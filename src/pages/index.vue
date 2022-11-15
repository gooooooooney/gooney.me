<script setup lang="ts">
import { formatDate } from '~/utils'
const router = useRouter()
const routes = router.getRoutes()
  .filter(v => v.name && v.path.startsWith('/posts'))
const posts = computed(() => routes.map(i => ({
  path: i.path,
  title: i.meta.frontmatter.title,
  date: i.meta.frontmatter.date,
  lang: i.meta.frontmatter.lang,
  duration: i.meta.frontmatter.duration,
})))

const getYear = (a: Date | string | number) => new Date(a).getFullYear()
const isSameYear = (a: Date | string | number, b: Date | string | number) => a && b && getYear(a) === getYear(b)
</script>

<template>
  <div>
    <template v-for="(post, idx) in posts" :key="post.path">
      <div v-if="!isSameYear(post.date, posts[idx - 1]?.date)">
        <h2>{{ getYear(post.date) }}</h2>
      </div>
      <app-link :to="post.path" class="mt-2 duration-300 transition-all ease-linear cursor-pointer text-[#666] dark:text-[#c9c6c6] hover:(decoration-none dark:text-white text-black) decoration-none">
        <h6 m-0>
          {{ post.title }}
        </h6>
        <p mt-0 text-sm>
          <span>{{ formatDate(post.date) }}</span>
          <span ml-2>{{ post.duration }}</span>
        </p>
      </app-link>
    </template>
  </div>
</template>

<!-- <route lang="yaml">
meta:
  layout: home
</route> -->
