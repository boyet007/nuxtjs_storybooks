<template>
  <section class="container">
    <PostPreview v-for="post in posts" 
    :key="post.id" 
    :title="post.title"
    :excerpt="post.previewText"
    :thumbnailUrl="post.thumbnailUrl"
    :id="post.id" />
  </section>
</template>

<script>
import PostPreview from '@/components/Blog/PostPreview'
export default {
  components: {
    PostPreview
  },
  asyncData(context) {
    return context.app.$storyapi.get('cdn/stories', {
      version: 'draft',
      starts_with: 'blog/'
    }).then(res => {
      console.log(res)
      return {
        posts: res.data.stories.map(bp => {
          return {
            id: bp.slug,
            title: bp.content.title,
            previewText: bp.content.summary,
            thumbnailUrl: bp.content.thumbnail
          }
      })}
    })
  },
  mounted() {

  }
  // data() {
  //   return {
  //     posts: [{
  //       title: 'A New begining',
  //       previewText: 'This will awesome, don\'t miss it!',
  //       thumbnailUrl: 'https://media-cdn.tripadvisor.com/media/photo-s/0b/c5/5e/da/pizza-hut.jpg',
  //       id: 'a-new-beginning'
  //     },
  //     {
  //       title: 'A second begining',
  //       previewText: 'This will second, don\'t miss it!',
  //       thumbnailUrl: 'https://2.bp.blogspot.com/-6rl8LGKtvqw/VqQeN3WUvfI/AAAAAAAAAgM/0QCpKnHEOkw/s320/Resep-Cara-Membuat-Sop-Iga-Sapi-Bening-1.jpg',
  //       id: 'a-second-beginning'
  //     }]
  //   }
  //}
}
</script>

<style scoped>
  #posts {
    padding-top: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
</style>
