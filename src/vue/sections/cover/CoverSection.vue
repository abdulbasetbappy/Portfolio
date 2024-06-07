<template>
  <SectionTemplate class="parent" :section-data="props.sectionData">
    <div class="resume">
      <button class="resume-btn">
        Resume
        <span>
            <i class="fa-solid fa-cloud-arrow-down"></i>
        </span>
      </button>
    </div>
    <!-- Title -->
    <h1 class="cover-title display-1" v-html="coverTitle" />

    <!-- Divider -->
    <hr class="solid-divider ms-1 me-1" />

    <!-- Info Items -->
    <InlineList
      class="info-list"
      :items="props.sectionData.content['items']['contactListItems']"
    />

    <!-- Description -->
    <p
      class="cover-description lead text-normal mb-4 mb-md-5"
      v-html="props.sectionData.content['locales']['bio']"
    />

    <!-- Social Links -->
    <SocialLinks :items="props.sectionData.content['items']['socialCircles']" />
  </SectionTemplate>
</template>

<script setup>
import SectionTemplate from "../_templates/SectionTemplate.vue";
import { computed } from "vue";
import { useData } from "../../../composables/data.js";
import { useNavigation } from "../../../composables/navigation.js";
import InlineList from "../../widgets/InlineList.vue";
import SocialLinks from "../../widgets/SocialLinks.vue";

const data = useData();
const navigation = useNavigation();

/**
 * @property {Object} sectionData
 */
const props = defineProps({
  sectionData: Object,
});

/**
 * @type {ComputedRef<String>}
 */
const coverTitle = computed(() => {
  if (navigation.isAllAtOnceMode()) {
    return props.sectionData.content["locales"]["welcome"];
  } else {
    return props.sectionData.content["locales"]["welcomeShort"];
  }
});
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";

.cover-title {
  margin-bottom: 1rem;
  text-transform: uppercase;
  font-weight: bold;
}

.solid-divider {
  @include media-breakpoint-up($navigation-sidebar-breakpoint) {
    display: none;
  }
}

.info-list {
  @include generate-dynamic-styles-with-hash(
    (
      xxxl: (
        margin-bottom: 2.5rem,
      ),
      lg: (
        margin-bottom: 2rem,
      ),
      md: (
        margin-bottom: 1.2rem,
      ),
    )
  );
}
.parent {
  position: relative;
}
.resume {
  position: absolute;
  top: 25px;
  right: 30px;
  @include generate-dynamic-styles-with-hash(
    (
      xxxl: (
        margin-bottom: 2.5rem,
      ),
      lg: (
        margin-bottom: 2rem,
      ),
      md: (
        margin-bottom: 1.2rem,
      ),
    )
  );
}
.resume-btn {
  border: none;
  background: $dark;
  padding: 5px 8px;
  border-radius: 8px;
    color: white;
    font-size: large;
  span {
    margin-left: 10px;
  }
  &:hover {
    background: $primary;
    transition: all 0.3s ease-in-out;
  }
}
.cover-description{
  color: gray !important;
}
</style>