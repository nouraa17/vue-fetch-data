<template>
  <div>
<!--    <nav>-->
<!--      <button @click="activeTab = 'posts'">Posts</button>-->
<!--      <button @click="activeTab = 'comments'">Comments</button>-->
<!--    </nav>-->
    <NavBar :activeTab="activeTab" @update:activeTab="activeTab = $event" />
<!--    <div v-if="activeTab === 'posts'">-->
<!--      <h1>Posts Data</h1>-->
<!--      <ListItems :data="posts" />-->
<!--    </div>-->

<!--    <div v-if="activeTab === 'comments'">-->
<!--      <h1>Comments Data</h1>-->
<!--      <ListItems :data="comments" />-->
<!--    </div>-->

    <h1>{{currentData.label}}</h1>
    <keep-alive>
      <component :is="ListItems" :data="currentData.data"></component>
    </keep-alive>
  </div>
</template>

<script>
import axios from "axios";
import NavBar from "@/components/NavBar.vue";
import ListItems from "@/components/ListItems.vue";

export default {
  components: {
    NavBar,
    ListItems,

  },
  data() {
    return {
      posts: [],
      comments:[],
      activeTab:'posts',

    };
  },
  computed:{
    ListItems() {
      return ListItems;
    },
    currentData() {
      return this.activeTab === 'posts'
          ? { data: this.posts, label: 'Posts Data' }
          : { data: this.comments, label: 'Comments Data' };
    }
  },
  mounted() {
    this.fetchPosts();
    this.fetchComments();
  },
  methods: {
    async fetchPosts() {
      try {
        let api_call = await axios.get('https://jsonplaceholder.typicode.com/posts');
        this.posts = api_call?.data;
      } catch (error) {
        console.error('Error fetching users:', error);
      }
    },
    async fetchComments() {
      try {
        let api_call = await axios.get('https://jsonplaceholder.typicode.com/posts/1/comments');
        this.comments = api_call?.data;
      } catch (error) {
        console.error('Error fetching users:', error);
      }
    },
  }
};
</script>

<style scoped>
  h1{
    margin-left: 7% !important;
    margin-bottom: 15px;
  }

</style>