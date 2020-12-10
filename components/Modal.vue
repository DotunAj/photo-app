<template>
  <div class="modal">
    <span class="modal__close" @click="close">

      <img src="@/assets/svg/times.svg" svg-inline>
    </span>
    <div class="modal__content">
      <div class="modal__content-img-container">
        <img :src="photo.urls.regular" :alt="photo.alt_description">

        <div class="bottom">
          <h5>
            {{ photo.user.name }}
          </h5>
          <p>{{ photo.user.location || 'unknown' }}</p>
        </div>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  props: {
    close: Function,
    photo: Object
  }

}
</script>
