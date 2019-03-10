<template>
  <section id="posts">
    <PostPreview
      v-for="post in posts"
      :key="post.id"
      :title="post.title"
      :excerpt="post.previewText"
      :thumbnailImage="post.thumbnailUrl"
      :id="post.id"
    />
  </section>
</template>

<script>
import PostPreview from '@/components/Blog/PostPreview';

export default {
  components: {
    PostPreview
  },
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "blog/"
      })
      .then(res => {
        return {
          posts: res.data.stories.map(bp => {
            return {
              id: bp.slug,
              title: bp.content.title,
              previewText: bp.content.summary,
              thumbnailUrl: bp.content.thumbnail
            };
          })
        };
      });
  }
  /*data(){
    return{
      posts:[
        {
          title:'A new Beginning',
          previewText: 'This will be awesome, dont miss it!',
          thumbnailUrl: 'https://d2lhw32459hxui.cloudfront.net/files/uploads/drupal/uploads/2016/12/tastyfoods.png',
          id: 'a-new-beginning'
        },
        {
          title:'A Second Beginning',
          previewText: 'This will be awesome, dont miss it!',
          thumbnailUrl: 'https://image.winudf.com/v2/image/Y29tLmhhYmliaS5UYXN0eWFuZFl1bW15Rm9vZFJlY2lwZV9zY3JlZW5fOF8xNTE0MTkwNzYwXzA3OA/screen-8.jpg?h=800&fakeurl=1&type=.jpg',
          id: 'a-second-beginning'
        }
      ]
    }
  }*/
};
</script>

<style scoped>
  #posts{
    padding-top: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  @media (min-width: 35rem) {
    #posts{
      flex-direction: row;
    }
  }
</style>

<style>
.container {
  min-height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

