<template>
  <div class="home-page">
    <section class="intro">
      <h1>Get the latest tech news!</h1>
    </section>
    <PostList :posts="loadedPosts" />
  </div>
</template>

<script>
import PostList from "@/components/Posts/PostList";

export default {
  components: {
    PostList
  },
  data() {
    return {
      //loading static data
      loadedPosts: [
        // {
        //   id: "1",
        //   title: "First Post",
        //   previewText: "This is our first post!",
        //   thumbnail:
        //     "https://static.pexels.com/photos/270348/pexels-photo-270348.jpeg"
        // },
        // {
        //   id: "2",
        //   title: "Second Post",
        //   previewText: "This is our second post!",
        //   thumbnail:
        //     "https://static.pexels.com/photos/270348/pexels-photo-270348.jpeg"
        // }
      ]
    };
  },
  created() {
    //suppose getting datat from backend but loaded on the client side
    // in this case page loaded first with static content and then render dynamic data back to the client
    // to remove this problem use asyncData() which execute on the server
    /*setTimeout(() => {
      this.loadedPosts = [
        {
          id: "1",
          title: "First Post",
          previewText: "This is our first post!",
          thumbnail:
            "https://static.pexels.com/photos/270348/pexels-photo-270348.jpeg"
        },
        {
          id: "2",
          title: "Second Post",
          previewText: "This is our second post!",
          thumbnail:
            "https://static.pexels.com/photos/270348/pexels-photo-270348.jpeg"
        }
      ];
    }, 1500);*/
  },
  asyncData(
    { isDev, route, store, env, params, query, req, res, redirect, error },
    callback
  ) {
    //executed on the server
    //get prerender the complete page back to the client
    // this will not work becuse this executed before the page render so will not use this.loadedPosts
    // only use for pages not for component, layout etc
    setTimeout(() => {
      // simple retun statement will not work
      //this function should return promise or callback
      callback(null, {
        loadedPosts: [
          {
            id: "1",
            title: "First Post",
            previewText: "This is our first post!",
            thumbnail:
              "https://static.pexels.com/photos/270348/pexels-photo-270348.jpeg"
          },
          {
            id: "2",
            title: "Second Post",
            previewText: "This is our second post!",
            thumbnail:
              "https://static.pexels.com/photos/270348/pexels-photo-270348.jpeg"
          }
        ]
      });
    }, 1500);
  }
};
</script>


<style scoped>
.intro {
  height: 300px;
  position: relative;
  padding: 30px;
  box-sizing: border-box;
  background-image: url("~assets/images/main-page-background.jpg");
  background-position: center;
  background-size: cover;
}

.intro h1 {
  position: absolute;
  top: 10%;
  left: 5%;
  width: 90%;
  font-size: 1.5rem;
  color: black;
  background-color: rgb(211, 211, 211);
  padding: 10px;
  border-radius: 10px;
  box-shadow: 3px 3px 3px black;
  box-sizing: border-box;
  border: 1px solid black;
}

@media (min-width: 768px) {
  .intro h1 {
    font-size: 2rem;
  }
}

.featured-posts {
  display: flex;
  padding: 20px;
  box-sizing: border-box;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}
</style>
