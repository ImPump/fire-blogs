<template>
  <div class="blog-card-wrap">
    <div class="blog-cards container">
      <div class="toggleEdit">
        <span>切换编辑按钮</span>
        <input type="checkbox" v-model="editPost" />
      </div>
      <BlogCard
        :post="post"
        v-for="(post, index) in sampleBlogCards"
        :key="index"
      />
      <BlogCard
        :post="post"
        v-for="(post, index) in blogPosts"
        :key="index"
      />
    </div>
  </div>
</template>

<script>
import BlogCard from "../components/BlogCard.vue";
export default {
  name: "blogs",
  components: {
    BlogCard,
  },
  computed: {
    sampleBlogCards() {
      return this.$store.state.sampleBlogCards;
    },
    blogPosts() {
      return this.$store.state.blogPosts;
    },
    editPost:{
        get(){
            return this.$store.state.editPost
        },
        set(payload){
            this.$store.commit('toggleEditPost', payload)
        }
    }
  },
  beforeDestroy () {
      this.$store.commit("toggleEditPost",false);
  }
};
</script>

<style lang="scss" scoped>
.blog-cards {
  position: relative;
  .toggleEdit {
    display: flex;
    align-items: center;
    position: absolute;
    top: -70px;
    right: 0;
    span {
      margin-right: 10px;
      color: #555;
      letter-spacing: 2px;
    }
    input[type="checkbox"] {
      position: relative;
      border: none;
      appearance: none;
      background: #fff;
      outline: none;
      width: 80px;
      height: 30px;
      border-radius: 20px;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
        0 2px 4px -1px rgba(0, 0, 0, 0.06);
    }
    input[type="checkbox"]::before {
      content: "";
      position: absolute;
      width: 30px;
      height: 30px;
      top: 0;
      left: 0;
      background-color: #303030;
      transform: scale(1.1);
      border-radius: 20px;
      transition: 300ms ease all;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
        0 2px 4px -1px rgba(0, 0, 0, 0.06);
    }
    input:checked[type="checkbox"]::before {
      background-color: #fff;
      left: 52px;
    }
  }
}
</style>