<template>
  <div>
    <transition name="fade">
      <Modal v-if="modalShown" :photo="modalPhoto" :close="closeModal" />
    </transition>
    <SearchBanner :show-search="true" />

    <div class="home">
      <div class="container ">
        <div class="home__container">
          <div v-if="loading" class="photo-grid">
            <div
              v-for="n in 6"
              :key="n"
              class="photo-grid__item shine placeholder"
              :class="`span-${Math.floor(Math.random() * 3) + 1}`"
            >
              <div class="photo-grid__item-line" />
              <div class="photo-grid__item-line short" />
            </div>
          </div>

          <div v-else class="photo-grid">
            <div
              v-for="photo in photos"
              :key="photo.id"
              class="photo-grid__item"
              :class="`span-${Math.floor(Math.random() * 3) + 1}`"
              @click="openModal(photo)"
            >
              <img :src="photo.urls.small" :alt="photo.alt_description">
              <div class="details">
                <h5>
                  {{ photo.user.name }}
                </h5>
                <p>{{ photo.user.location }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      modalShown: false,
      loading: true,
      photos: [],
      modalPhoto: {},
      search: ''
    }
  },

  async created () {
    const photos = await this.$axios.$get('search/photos?query=African', {
      headers: {
        Authorization: `Client-ID ${process.env.ACCESS_KEY}`
      }
    })
    this.photos = photos.results
    this.loading = false
  },

  methods: {
    openModal (photo) {
      this.modalPhoto = photo
      this.modalShown = true
    },

    closeModal () {
      this.modalShown = false
    }
  }
}
</script>
