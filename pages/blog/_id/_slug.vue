<template>
  <section>
    <header class="bg-white shadow">
      <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
        <h1 class="text-3xl font-bold leading-tight text-gray-900">{{ post.title }}</h1>
      </div>
    </header>
    <main>
      <div class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
        <!-- Replace with your content -->
        <div class="px-4 py-4 sm:px-0">
          <b>{{ user.name }}</b>
          <p>{{ post.body }}</p>
        </div>
        <hr />
        <p><nuxt-link class="btn btn-blue" to="/blog">Volver</nuxt-link></p>
        <!-- /End replace -->
      </div>
    </main>
  </section>
</template>


<script>
  export default {
    head(){
      return {
        titleTemplate: '%s - Ynsitu',
        title: this.title
      }
    },
    async asyncData({ params, $axios }) {
      try {
        const post = await $axios.get(`https://jsonplaceholder.typicode.com/posts/${params.id}`)
        const user = await $axios.get(`https://jsonplaceholder.typicode.com/users/${post.data.userId}`)

        return {
          post: post.data,
          user: user.data,
          title: post.data.title,
        }
      } catch (error) {
        return {
          post: [],
          user: [],
          title: 'ERROR',
        }
      }
    }
  }
</script>
