<template>
  <div>


    <nav class="navbar navbar-expand-lg navbar-light bg-light mb-4">
      <div class="container">
        <a class="navbar-brand" href="#">Data Viewer</a>
        <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarNavAltMarkup"
            aria-controls="navbarNavAltMarkup"
            aria-expanded="false"
            aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
          <div class="navbar-nav">
            <a class="nav-link"
                :class="{ active: activeTab === 'posts' }"
                href="#"
                @click.prevent="selectTab('posts')">Posts</a>
            <a class="nav-link"
                :class="{ active: activeTab === 'comments' }"
                href="#"
                @click.prevent="selectTab('comments')">Comments</a>
          </div>
        </div>
      </div>
    </nav>


  </div>
</template>

<script>
export default {
  name:'NavBar',
  props: {
    activeTab: {
      type: String,
      required: true,
    },
  },
  methods:{
    selectTab(tab) {
      this.$emit('update:activeTab', tab);
    },
  }
}
</script>

<style scoped>

</style>