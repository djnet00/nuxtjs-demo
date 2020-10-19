<template>
  <section>
    <header class="bg-white shadow">
      <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
        <h1 class="text-3xl font-bold leading-tight text-gray-900">Blog</h1>
      </div>
    </header>
    <main>
      <div class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
        <!-- Replace with your content -->
        <div class="px-4 py-4 sm:px-0">
          <ul class="list-disc">
            <li class="relative -mb-px block border p-4 border-grey"
              v-for="post in posts" :key="post.id">
              <nuxt-link :to="`/blog/${post.id}/${ dashify(post.title)}`">{{ post.title }}</nuxt-link>
            </li>
          </ul>
        </div>
        <!-- /End replace -->
      </div>
    </main>
  </section>
</template>

<script>
  import dashify from "dashify"

  export default {
    data(){
      return{
        posts:[],
        title: '',
        dashify: dashify
      }
    },
    head(){
      return {
        titleTemplate: '%s - Ynsitu',
        title: this.title
      }
    },
    async asyncData({ params, $axios }) {
      const res = await $axios.get('https://jsonplaceholder.typicode.com/posts')

      return { posts: res.data, title: 'Blog Listado de Posts' }
    }
  }
</script>
