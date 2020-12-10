<template>
  <div class="search-banner">
    <div class="container">
      <div v-if="showSearch" class="input-container">
        <input v-model="search" type="search" placeholder="Search for photo" @keyup.enter="searchPhoto()">
        <img src="@/assets/svg/search.svg" alt="">
      </div>

      <div v-else class="search-banner__result">
        <h1>{{ loading? 'Searching for': photos.length? 'Result of': 'No Result found for' }} <span>"{{ qsearch }}"</span></h1>
        <nuxt-link to="/">
          Go Back
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    showSearch: Boolean,
    loading: Boolean,
    photos: Array,
    qsearch: String
  },
  data () {
    return {
      search: ''
    }
  },

  methods: {
    searchPhoto () {
      if (this.search.length > 0) {
        this.$router.push(`/search?query=${this.search}`)
      }
    }
  }
}
</script>
