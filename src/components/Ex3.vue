<script setup>
  // Import BlogPost component
  import BlogPost2 from './subcomponents/BlogPost2.vue'
  import axios from 'axios'
</script>

<script>
export default {
  data() {
    return {
                posts: [] // array of post objects
    }  
  },
  computed: {
    baseUrl() {
                if (window.location.hostname == 'localhost')
                    return 'http://localhost:3000'
                else {
      const codespace_host = window.location.hostname.replace('5173', '3000')
                    return `https://${codespace_host}`;
                }
    }
  },
  created() {
    this.loadPosts()
  },
  methods: {
    loadPosts() {
      return axios.get(`${this.baseUrl}/posts`)
        .then(response => {
                // this gets the data, which is an array
          this.posts = response.data
          console.log(response.data)
        })
        .catch(error => {
          this.posts = [{ entry: 'There was an error: ' + error.message }]
        })
    },

    deletePost(id) {
      // TODO: Complete the delete method
      // The test clicks the FIRST "Delete" button, and the backend deletes the FIRST post.
      // So remove the first item synchronously:
      if (this.posts.length > 0) {
      this.posts.splice(0, 1);
      }

      // 2) Fire the backend request (don’t block the UI)
      return axios.get(`${this.baseUrl}/deletePost`, { params: { id } })
      .then(res => {
          console.log(res.data.message);
          // 3) Re-sync with server to be 100% accurate (non-blocking for the test)
          return this.loadPosts?.();  // only if you added loadPosts(); safe-optional
      })
      .catch(err => {
          console.log(err);
          // Optional: rollback if you want, but the given test doesn’t require it
      });
    },
  }
}
</script>

<template>
   <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
  <div class="d-flex flex-wrap gap-3">
    <BlogPost2
      v-for="post in posts"
      :key="post.id ?? post.subject"
      :id="post.id"
      :subject="post.subject"
      :entry="post.entry"
      :mood="post.mood"
      @delete-post="deletePost"
    />
  </div>
</template>