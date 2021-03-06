<template>
  <div class="k-file-preview">
    <k-view class="k-file-preview-layout">
      <div class="k-file-preview-image">
        <a
          v-tab
          :href="file.url"
          :title="$t('open')"
          class="k-file-preview-image-link"
          target="_blank"
        >
          <k-image
            v-if="file.panelImage && file.panelImage.url"
            :src="file.panelImage.url"
            back="none"
          />
          <k-icon
            v-else-if="file.panelIcon"
            :type="file.panelIcon.type"
            :style="{ color: file.panelIcon.color }"
            class="k-file-preview-icon"
          />
          <span v-else class="k-file-preview-placeholder" />
        </a>
      </div>
      <div class="k-file-preview-details">
        <ul>
          <li>
            <h3>{{ $t("template") }}</h3>
            <p>{{ file.template || "—" }}</p>
          </li>
          <li>
            <h3>{{ $t("mime") }}</h3>
            <p>{{ file.mime }}</p>
          </li>
          <li>
            <h3>{{ $t("url") }}</h3>
            <p>
              <k-link :to="file.url" tabindex="-1" target="_blank">/{{ file.id }}</k-link>
            </p>
          </li>
          <li>
            <h3>{{ $t("size") }}</h3>
            <p>{{ file.niceSize }}</p>
          </li>
          <li>
            <h3>{{ $t("dimensions") }}</h3>
            <p v-if="file.dimensions">{{ file.dimensions.width }}&times;{{ file.dimensions.height }} {{ $t("pixel") }}</p>
            <p v-else>—</p>
          </li>
          <li>
            <h3>{{ $t("orientation") }}</h3>
            <p v-if="file.dimensions">{{ $t("orientation." + file.dimensions.orientation) }}</p>
            <p v-else>—</p>
          </li>
        </ul>
      </div>
    </k-view>
  </div>
</template>

<script>
export default {
  props: {
    file: Object
  },
};
</script>
<style lang="scss">
.k-file-preview {
  background: lighten($color-dark, 10%);
}
.k-file-preview-layout {
  display: grid;

  @media screen and (max-width: $breakpoint-medium) {
    padding: 0 !important;
  }

  @media screen and (min-width: $breakpoint-small) {
    grid-template-columns: 50% auto;
  }
  @media screen and (min-width: $breakpoint-medium) {
    display: flex;
    align-items: center;
  }
}
.k-file-preview-layout > * {
  min-width: 0;
}
.k-file-preview-image {
  position: relative;
  background: url($pattern);

  @media screen and (min-width: $breakpoint-medium) {
    width: 33.33%;
  }
  @media screen and (min-width: $breakpoint-large) {
    width: 25%;
  }
}

.k-file-preview-image .k-image span {
  overflow: hidden;
  padding-bottom: 66.66%;

  @media screen and (min-width: $breakpoint-small) and (max-width: $breakpoint-medium) {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    padding-bottom: 0 !important;
  }

  @media screen and (min-width: $breakpoint-medium) {
    padding-bottom: 100%;
  }
}
.k-file-preview-placeholder {
  display: block;
  padding-bottom: 100%;
}
.k-file-preview-image img {
  padding: 3rem;
}

.k-file-preview-image-link {
  display: block;
  outline: 0;
}
.k-file-preview-image-link[data-tabbed] {
  outline: 2px solid $color-focus !important;
  outline-offset: -2px;
}

.k-file-preview-icon {
  position: relative;
  display: block;
  padding-bottom: 100%;
  overflow: hidden;
  color: rgba($color-white, 0.5);
}
.k-file-preview-icon svg {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(4);
}
.k-file-preview-details {
  padding: 1.5rem;
  flex-grow: 1;

  @media screen and (min-width: $breakpoint-medium) {
    padding: 3rem;
  }
}
.k-file-preview-details ul {
  line-height: 1.5em;
  max-width: 50rem;
  display: grid;
  grid-gap: 1.5rem 3rem;
  grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));

  @media screen and (min-width: $breakpoint-small) {
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  }
}
.k-file-preview-details h3 {
  font-size: $font-size-small;
  font-weight: 500;
  color: $color-light-grey;
}
.k-file-preview-details p {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  color: rgba($color-white, 0.75);
  font-size: $font-size-small;
}
.k-file-preview-details p a {
  display: block;
  width: 100%;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
